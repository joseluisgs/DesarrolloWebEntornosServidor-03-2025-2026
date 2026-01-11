- [6. Pruebas en Aplicaciones Spring MVC](#6-pruebas-en-aplicaciones-spring-mvc)
    - [6.1 Fundamentos de Testing en Spring](#61-fundamentos-de-testing-en-spring)
    - [6.2 Pruebas de Controladores con MockMvc](#62-pruebas-de-controladores-con-mockmvc)
    - [6.3 Pruebas de Servicios y Repositorios](#63-pruebas-de-servicios-y-repositorios)
    - [6.4 Configuración de Tests](#64-configuración-de-tests)

# 6. Pruebas en Aplicaciones Spring MVC

## 6.1 Fundamentos de Testing en Spring

El testing es una parte fundamental del desarrollo de software profesional. Spring Boot proporciona un ecosistema completo de herramientas para escribir pruebas que garanticen la calidad y correctitud de nuestra aplicación.

**Tipos de Pruebas:**

- **Pruebas Unitarias:** Verifican que una unidad de código (método, clase) funciona correctamente de forma aislada. Se usan **mocks** para simular dependencias.
- **Pruebas de Integración:** Verifican que varias unidades de código funcionan correctamente juntas. Se usa el contexto real de Spring.
- **Pruebas End-to-End (E2E):** Simulan la interacción completa del usuario con la aplicación.

**Herramientas Principales:**

- **JUnit 5:** Framework de testing estándar para Java.
- **Mockito:** Framework para crear mocks.
- **Spring Test:** Módulos de Spring para testing.
- **AssertJ:** Librería de aserciones fluidas.
- **Hamcrest:** Matcher de aserciones.

**Anotaciones Importantes:**

```java
@SpringBootTest // Carga el contexto completo de Spring
@WebMvcTest(ProductoController.class) // Carga solo el contexto web para el controller
@DataJpaTest // Configuración específica para JPA/Repositories
@ExtendWith(SpringExtension.class) // Integración de JUnit 5 con Spring
@AutoConfigureMockMvc // Configura MockMvc automáticamente
@Test // Indica que es un método de prueba
@DisplayName("Descripción de la prueba")
```

📝 **Nota del Profesor**: Las pruebas son como los exámenes de la aplicación. Si no practicas (pruebas), no sabes si realmente sabes (el código funciona). ¡Testea siempre!

💡 **Tip del Examinador**: En el ciclo TDD (Test-Driven Development), primero se escribe el test, luego el código que pasa el test. Esto asegura que todo el código tiene su prueba.

## 6.2 Pruebas de Controladores con MockMvc

`MockMvc` es una herramienta poderosa que simula peticiones HTTP sin necesidad de levantar un servidor real. Permite probar el flujo completo del Controller.

**Estructura de un Test de Controller:**

```java
@WebMvcTest(ProductoController.class) // Carga solo el contexto web
@Import(TestSecurityConfig.class) // Si hay seguridad configurada
class ProductoControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @MockBean
    private ProductoService productoService;

    @MockBean
    private UserDetailsService userDetailsService;

    // Tests...
}
```

**Test de Petición GET exitosa:**

```java
@Test
@DisplayName("GET /productos - Devuelve lista de productos")
void testListarProductos_Success() throws Exception {
    // Given: Preparamos los datos
    List<Producto> productos = Arrays.asList(
        new Producto(1L, "iPhone", 999.99f),
        new Producto(2L, "Samsung", 899.99f)
    );
    when(productoService.findAll()).thenReturn(productos);

    // When & Then: Ejecutamos y verificamos
    mockMvc.perform(get("/productos")
            .contentType(MediaType.TEXT_HTML))
        .andExpect(status().isOk())
        .andExpect(view().name("productos/lista"))
        .andExpect(model().attributeExists("productos"))
        .andExpect(model().attribute("productos", hasSize(2)))
        .andExpect(content().string(containsString("iPhone")));
}
```

**Test de Petición GET con error 404:**

```java
@Test
@DisplayName("GET /productos/999 - Producto no encontrado")
void testDetalleProducto_NotFound() throws Exception {
    // Given
    when(productoService.findById(999L)).thenThrow(new ProductoNotFoundException(999L));

    // When & Then
    mockMvc.perform(get("/productos/{id}", 999L))
        .andExpect(status().isNotFound())
        .andExpect(view().name("error/404"))
        .andExpect(model().attributeExists("error"));
}
```

**Test de Formulario POST con validación:**

```java
@Test
@DisplayName("POST /productos/guardar - Validación fallida")
void testGuardarProducto_ValidationError() throws Exception {
    // Given: Producto con datos inválidos (nombre vacío)
    Producto productoInvalido = new Producto();
    productoInvalido.setNombre(""); // Violación de @NotEmpty
    productoInvalido.setPrecio(-10f); // Violación de @DecimalMin

    // When & Then
    mockMvc.perform(post("/productos/guardar")
            .contentType(MediaType.APPLICATION_FORM_URLENCODED)
            .param("nombre", "")
            .param("precio", "-10")
            .with(csrf())) // Token CSRF obligatorio
        .andExpect(status().isOk()) // Vuelve al formulario
        .andExpect(view().name("productos/form"))
        .andExpect(model().hasErrors())
        .andExpect(model().attributeHasFieldErrors("producto", "nombre", "precio"));
}
```

**Matchers Útiles:**

```java
// Status
.andExpect(status().isOk())
.andExpect(status().isNotFound())
.andExpect(status().isBadRequest())
.andExpect(status().isForbidden())

// Vista
.andExpect(view().name("productos/lista"))
.andExpect(forwardedUrl("/WEB-INF/views/productos/lista.jsp"))

// Model
.andExpect(model().attributeExists("productos"))
.andExpect(model().attribute("productos", hasSize(2)))
.andExpect(model().attributeHasFieldErrors("producto", "nombre", "precio"))

// Contenido
.andExpect(content().string(containsString("iPhone")))
.andExpect(content().contentType(MediaType.APPLICATION_JSON))
```

📝 **Nota del Profesor**: MockMvc permite probar Controllers sin levantar un servidor real. Es rápido y fiable. ¡La herramienta favorita para tests de Controller!

⚠️ **Advertencia**: Si tu aplicación usa Spring Security, debes añadir `.with(csrf())` a las peticiones POST/PUT/DELETE y mockear `UserDetailsService`.

## 6.3 Pruebas de Servicios y Repositorios

### Pruebas de Servicios

Los servicios contienen lógica de negocio y deben probarse de forma aislada, mockeando sus dependencias (repositorios).

```java
@ExtendWith(MockitoExtension.class)
class ProductoServiceTest {

    @Mock
    private ProductoRepository productoRepository;

    @InjectMocks
    private ProductoService productoService;

    @Test
    @DisplayName("findById - Producto existente")
    void testFindById_Existente() {
        // Given
        Producto productoEsperado = new Producto(1L, "iPhone", 999.99f);
        when(productoRepository.findById(1L)).thenReturn(Optional.of(productoEsperado));

        // When
        Producto resultado = productoService.findById(1L);

        // Then
        assertThat(resultado).isNotNull();
        assertThat(resultado.getNombre()).isEqualTo("iPhone");
        verify(productoRepository).findById(1L); // Verifica que se llamó al método
    }

    @Test
    @DisplayName("findById - Producto no existente")
    void testFindById_NoExistente() {
        // Given
        when(productoRepository.findById(999L)).thenReturn(Optional.empty());

        // When & Then
        assertThatThrownBy(() -> productoService.findById(999L))
            .isInstanceOf(ProductoNotFoundException.class);
    }

    @Test
    @DisplayName("save - Guarda producto correctamente")
    void testSave_ProductoValido() {
        // Given
        Producto producto = new Producto(null, "Nuevo Producto", 99.99f);
        Producto productoGuardado = new Producto(1L, "Nuevo Producto", 99.99f);
        
        when(productoRepository.save(any(Producto.class))).thenReturn(productoGuardado);

        // When
        Producto resultado = productoService.save(producto);

        // Then
        assertThat(resultado.getId()).isEqualTo(1L);
        assertThat(resultado.getNombre()).isEqualTo("Nuevo Producto");
        verify(productoRepository).save(producto);
    }
}
```

### Pruebas de Repositorios

Los repositorios deben probarse contra una base de datos real (o embebida como H2).

```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.ANY)
class ProductoRepositoryTest {

    @Autowired
    private ProductoRepository productoRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    @DisplayName("findByNombreContainsIgnoreCase - Encuentra productos por nombre")
    void testFindByNombreContainsIgnoreCase() {
        // Given
        entityManager.persist(new Producto(null, "iPhone 15", 999.99f));
        entityManager.persist(new Producto(null, "Samsung S24", 899.99f));
        entityManager.persist(new Producto(null, "iPad Pro", 1199.99f));
        entityManager.flush();

        // When
        List<Producto> resultados = productoRepository
            .findByNombreContainsIgnoreCase("iphone");

        // Then
        assertThat(resultados).hasSize(1);
        assertThat(resultados.get(0).getNombre()).isEqualTo("iPhone 15");
    }

    @Test
    @DisplayName("findByCategoria - Encuentra productos por categoría")
    void testFindByCategoria() {
        // Given
        Categoria tecnologia = new Categoria(1L, "Tecnología");
        entityManager.persist(tecnologia);
        
        entityManager.persist(new Producto(null, "Laptop", 1499.99f, tecnologia));
        entityManager.persist(new Producto(null, "Mouse", 29.99f, tecnologia));
        entityManager.persist(new Producto(null, "Zapatos", 99.99f)); // Sin categoría
        entityManager.flush();

        // When
        List<Producto> resultados = productoRepository.findByCategoria(tecnologia);

        // Then
        assertThat(resultados).hasSize(2);
    }
}
```

**Matchers de AssertJ Útiles:**

```java
assertThat(resultado).isNotNull();
assertThat(resultado).isInstanceOf(Producto.class);
assertThat(resultado.getNombre()).isEqualTo("iPhone");
assertThat(resultado.getNombre()).isNotEmpty();
assertThat(resultado.getPrecio()).isGreaterThan(0);
assertThat(resultado.getPrecio()).isBetween(100, 1000);
assertThat(lista).hasSize(2);
assertThat(lista).contains(producto1, producto2);
assertThat(lista).extracting(Producto::getNombre).contains("iPhone");
assertThatThrownBy(() -> service.findById(999L))
    .isInstanceOf(ProductoNotFoundException.class);
```

📝 **Nota del Profesor**: Los tests de Repository usan `@DataJpaTest` que configura automáticamente una base de datos H2 en memoria. ¡Tests rápidos y fiables!

## 6.4 Configuración de Tests

**Directorios de Tests:**

```
src/test/
├── java/com/ejemplo/app/
│   ├── Controller/
│   │   └── ProductoControllerTest.java
│   ├── Service/
│   │   └── ProductoServiceTest.java
│   └── Repository/
│       └── ProductoRepositoryTest.java
└── resources/
    ├── application-test.properties
    └── data.sql (datos de prueba)
```

**application-test.properties:**

```properties
# Perfil de test
spring.profiles.active=test

# H2 en memoria para tests
spring.datasource.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# JPA
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create-drop

# Mostrar SQL en tests
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

**Buenas Prácticas en Tests:**

1. **Naming:** Nombra los tests descriptivamente: `testMetodo_Condicion_Resultado()`
2. **AAA:** Arrange (preparar), Act (actuar), Assert (verificar)
3. **Aislamiento:** Cada test debe ser independiente
4. **Rapidez:** Los tests deben ejecutarse en milisegundos
5. **Fiabilidad:** No dependas de datos externos o estado global

💡 **Tip del Examinador**: En un proyecto profesional, aim para una cobertura de tests del 70-80%. No es necesario 100%, pero sí cubrir los casos críticos (Happy Path + Edge Cases).
