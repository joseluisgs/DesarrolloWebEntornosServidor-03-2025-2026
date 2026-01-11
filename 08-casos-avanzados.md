- [8. Casos Avanzados del Proyecto](#8-casos-avanzados-del-proyecto)
    - [8.1 GlobalControllerAdvice - Variables Globales](#81-globalcontrolleradvice---variables-globales)
    - [8.2 ModelAttribute - Datos Compartidos en Controller](#82-modelattribute---datos-compartidos-en-controller)
    - [8.3 Email Asíncrono - Evitar Bloqueos](#83-email-asíncrono---evitar-bloqueos)
    - [8.4 Gestión de Archivos - Upload y Storage](#84-gestión-de-archivos---upload-y-storage)
    - [8.5 Generación de PDF al Vuelo](#85-generación-de-pdf-al-vuelo)

# 8. Casos Avanzados del Proyecto

## 8.1 GlobalControllerAdvice - Variables Globales

El `@ControllerAdvice` es una herramienta poderosa para compartir datos entre todas las vistas sin repetir código en cada Controller.

```java
@ControllerAdvice
public class GlobalControllerAdvice {
    
    @Autowired
    private MessageSource messageSource;
    
    @Autowired
    private UserService userService;
    
    @ModelAttribute("isAuthenticated")
    public boolean isAuthenticated(Authentication auth) {
        return auth != null && auth.isAuthenticated() 
            && !"anonymousUser".equals(auth.getName());
    }
    
    @ModelAttribute("currentUser")
    public User getCurrentUser() {
        if (isAuthenticated(SecurityContextHolder.getContext().getAuthentication())) {
            String email = SecurityContextHolder.getContext().getAuthentication().getName();
            return userService.buscarPorEmail(email);
        }
        return null;
    }
    
    @ModelAttribute("isAdmin")
    public boolean isAdmin() {
        Authentication auth = SecurityContextHolder.getContext().getAuthentication();
        return auth.getAuthorities().stream()
                .anyMatch(a -> a.getAuthority().equals("ADMIN"));
    }
    
    @ModelAttribute("message")
    public Function<String, String> messageFunction() {
        return key -> messageSource.getMessage(key, null, LocaleContextHolder.getLocale());
    }
}
```

## 8.2 ModelAttribute - Datos Compartidos en Controller

Dentro de un Controller específico, podemos usar `@ModelAttribute` para compartir datos entre todos los métodos.

```java
@Controller
@RequestMapping("/app")
public class PurchaseController {
    
    @Autowired
    HttpSession session;
    
    @Autowired
    ProductService productoServicio;
    
    @ModelAttribute("carrito")
    public List<Product> productosCarrito() {
        @SuppressWarnings("unchecked")
        List<Long> contenido = (List<Long>) session.getAttribute("carrito");
        return (contenido == null) ? null : productoServicio.variosPorId(contenido);
    }
    
    @ModelAttribute("total_carrito")
    public Double totalCarrito() {
        List<Product> productosCarrito = productosCarrito();
        if (productosCarrito != null) {
            return productosCarrito.stream()
                    .mapToDouble(Product::getPrecio)
                    .sum();
        }
        return 0.0;
    }
    
    @GetMapping("/carrito")
    public String verCarrito(Model model) {
        return "app/compra/carrito";
    }
}
```

## 8.3 Email Asíncrono - Evitar Bloqueos

El envío de emails puede ser lento. Usar un hilo separado mejora la experiencia del usuario.

```java
@Service
public class EmailService {
    
    @Autowired
    private JavaMailSender mailSender;
    
    public void enviarEmailConfirmacionCompra(Purchase compra) {
        try {
            MimeMessage message = mailSender.createMimeMessage();
            MimeMessageHelper helper = new MimeMessageHelper(message, true, "UTF-8");
            
            helper.setFrom("noreply@waladaw.com");
            helper.setTo(compra.getPropietario().getEmail());
            helper.setSubject("Confirmación de Compra #" + compra.getId());
            
            String htmlContent = construirEmailHTML(compra);
            helper.setText(htmlContent, true);
            
            mailSender.send(message);
        } catch (Exception e) {
            logger.error("Error al enviar email: " + e.getMessage());
        }
    }
}

// En el controller - Envío asíncrono
@GetMapping("/carrito/finalizar")
public String checkout() {
    Purchase compra = compraServicio.insertar(new Purchase(), usuario);
    productos.forEach(p -> compraServicio.addProductoCompra(p, compra));
    
    // Enviar email en un thread separado
    new Thread(() -> {
        try {
            emailService.enviarEmailConfirmacionCompra(compra);
        } catch (Exception e) {
            logger.error("Error enviando email: " + e.getMessage());
        }
    }).start();
    
    return "redirect:/app/miscompras/factura/" + compra.getId();
}
```

## 8.4 Gestión de Archivos - Upload y Storage

```java
@Service
public class FileSystemStorageService implements StorageService {
    
    private final Path rootLocation;
    
    public String store(MultipartFile file) {
        try {
            if (file.isEmpty()) {
                throw new StorageException("Archivo vacío");
            }
            
            String filename = StringUtils.cleanPath(file.getOriginalFilename());
            String extension = filename.substring(filename.lastIndexOf("."));
            String storedFilename = UUID.randomUUID().toString() + extension;
            
            Path destinationFile = this.rootLocation.resolve(storedFilename);
            Files.copy(file.getInputStream(), destinationFile);
            
            return storedFilename;
        } catch (IOException e) {
            throw new StorageException("Error al guardar archivo", e);
        }
    }
}

// En el controller
@PostMapping("/misproducto/nuevo/submit")
public String nuevoProductoSubmit(
        @Valid @ModelAttribute Product producto,
        @RequestParam("file") MultipartFile file,
        BindingResult bindingResult) {
    
    if (bindingResult.hasErrors()) {
        return "app/producto/ficha";
    }
    
    if (!file.isEmpty()) {
        String imagen = storageService.store(file);
        producto.setImagen(MvcUriComponentsBuilder
            .fromMethodName(FilesController.class, "serveFile", imagen)
            .build().toUriString());
    }
    
    producto.setPropietario(usuario);
    productoServicio.insertar(producto);
    return "redirect:/app/misproductos";
}
```

## 8.5 Generación de PDF al Vuelo

```java
@Controller
@RequestMapping("/app")
public class PurchaseController {
    
    @Autowired
    Html2PdfService documentGeneratorService;
    
    @RequestMapping(
        value = "/miscompras/factura/{id}/pdf",
        method = RequestMethod.GET,
        produces = MediaType.APPLICATION_PDF_VALUE
    )
    public ResponseEntity<InputStreamResource> facturaPDF(@PathVariable Long id) {
        Purchase compra = compraServicio.buscarPorId(id);
        List<Product> productos = productoServicio.productosDeUnaCompra(compra);
        Double total = productos.stream().mapToDouble(Product::getPrecio).sum();
        
        ByteArrayInputStream bis = GeneradorPDF.factura2PDF(compra, productos, total);
        
        HttpHeaders headers = new HttpHeaders();
        headers.add("Content-Disposition", "inline; filename=factura_" + compra.getId() + ".pdf");
        
        return ResponseEntity
                .ok()
                .headers(headers)
                .contentType(MediaType.APPLICATION_PDF)
                .body(new InputStreamResource(bis));
    }
}
```

📝 **Nota del Profesor**: Estos casos avanzados muestran cómo resolver problemas reales en proyectos profesionales. ¡Estudiadlos bien!
