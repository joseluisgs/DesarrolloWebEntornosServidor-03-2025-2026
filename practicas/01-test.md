## Test de Desarrollo Web Dinámico (Spring Boot, MVC y Pebble)

- [Test de Desarrollo Web Dinámico (Spring Boot, MVC y Pebble)](#test-de-desarrollo-web-dinámico-spring-boot-mvc-y-pebble)
  - [I. Arquitectura y Fundamentos de Spring MVC](#i-arquitectura-y-fundamentos-de-spring-mvc)
  - [II. GlobalControllerAdvice y Variables Globales](#ii-globalcontrolleradvice-y-variables-globales)
  - [III. Pebble Template Engine](#iii-pebble-template-engine)
  - [IV. Estado, Seguridad y Formularios](#iv-estado-seguridad-y-formularios)


### I. Arquitectura y Fundamentos de Spring MVC

1. ¿Cuál de los siguientes no es un componente fundamental del patrón de diseño Model-View-Controller (MVC)?
    A) Modelo
    B) Vista
    C) Controlador
    D) Servicio (Service Layer)

2. En el patrón MVC, ¿cuál es la principal función del componente Controlador?
    A) Presentar los datos al usuario (HTML)
    B) Representar los datos y la lógica de negocio
    C) Manejar las peticiones HTTP y coordinar Model y View
    D) Almacenar información de sesión en el servidor

3. En el flujo de una petición en Spring MVC, ¿qué componente actúa como el "servlet frontal" que recibe todas las peticiones HTTP y las delega?
    A) View Resolver
    B) DispatcherServlet
    C) Handler Mapping
    D) ProductoController

4. ¿Cuál de los siguientes enfoques para pasar datos del Controller a la Vista es considerado el más moderno, limpio y la opción recomendada por defecto en Spring MVC?
    A) HttpServletResponse
    B) ModelAndView
    C) RedirectAttributes
    D) Model

5. ¿Para qué se utiliza la anotación `@Controller` en una clase Java?
    A) Definir la lógica de negocio (Service Layer)
    B) Mapear una entidad a una tabla de base de datos
    C) Manejar las peticiones HTTP y actuar como director de tráfico
    D) Recibir peticiones REST y devolver JSON

6. La diferencia clave entre la ejecución de código en el Servidor (Java) y la ejecución en el Cliente (JavaScript) es que el código del Servidor:
    A) Puede manipular el DOM del navegador
    B) Se puede ver y manipular fácilmente por el usuario
    C) Es usado solo para validación instantánea de formularios
    D) Accede de forma segura a la Base de Datos y ejecuta la lógica de negocio

7. ¿Cuál es la anotación de Spring MVC utilizada para vincular automáticamente los datos de un formulario (POST) a un objeto Java (POJO)?
    A) `@PathVariable`
    B) `@RequestParam`
    C) `@ModelAttribute`
    D) `@Autowired`

8. El principal objetivo de utilizar el patrón Post-Redirect-Get (PRG) después de procesar un formulario POST es:
    A) Permitir el uso de Flash Attributes
    B) Optimizar la velocidad de la base de datos
    C) Prevenir el reenvío accidental del formulario si el usuario refresca la página
    D) Configurar el código de estado HTTP 200 OK

9. Cuando se usa una redirección (`return "redirect:/ruta";`), ¿qué objeto de Spring se utiliza para enviar mensajes o datos temporales que sobreviven esa única redirección?
    A) Model
    B) HttpSession
    C) ModelAndView
    D) RedirectAttributes

10. Dentro del Modelo (lógica de negocio), ¿cuál es la capa que encapsula la lógica de negocio, aplica las reglas y orquesta los repositorios?
    A) Controller
    B) Entity
    C) Repository
    D) Service

11. En el flujo de Spring MVC, ¿cuál es el componente encargado de tomar el nombre lógico de la vista (`"productos/lista"`) y traducirlo a la ruta del archivo físico (`src/main/resources/templates/productos/lista.peb`)?
    A) DispatcherServlet
    B) Handler Mapping
    C) View Resolver
    D) ProductoController

12. ¿Qué anotación de Spring MVC se utiliza en un método de un Controller para extraer una variable de la propia URL, como el `id` en `/productos/{id}`?
    A) `@RequestParam`
    B) `@RequestBody`
    C) `@PathVariable`
    D) `@SessionAttribute`

13. ¿Cuál es la tecnología o "muro de filtros" considerada el estándar de la industria en Java para gestionar la autentificación y la autorización?
    A) Hibernate Validator
    B) Apache Tomcat
    C) Spring Security
    D) Pebble Template Engine

### II. GlobalControllerAdvice y Variables Globales

14. ¿Cuál es el objetivo principal de la clase anotada con `@ControllerAdvice` (`GlobalControllerAdvice`)?
    A) Validar formularios con Bean Validation
    B) Gestionar la lógica de negocio específica de un solo Controller
    C) Inyectar automáticamente variables comunes en todas las vistas del proyecto
    D) Convertir objetos Java a formato JSON (REST)

15. Además de inyectar atributos globales, ¿qué otra funcionalidad permite la anotación `@ControllerAdvice` en Spring?
    A) Definir el *timeout* de la sesión HTTP
    B) Manejar excepciones de forma global
    C) Traducir el nombre de la vista (View Resolving)
    D) Generar tokens CSRF para peticiones GET

16. ¿Qué variable global de tipo `User` (o `null`) proporciona información sobre el usuario actualmente autenticado?
    A) `isAuthenticated`
    B) `username`
    C) `isAdmin`
    D) `currentUser`

17. Dentro de la clase `GlobalControllerAdvice`, ¿qué anotación de método se utiliza para asegurar que el resultado de ese método se añada automáticamente al Model de *todas* las peticiones?
    A) `@GetMapping`
    B) `@Controller`
    C) `@ModelAttribute`
    D) `@Autowired`

18. ¿Qué dos variables globales están relacionadas con la protección CSRF y son necesarias en los formularios de la vista?
    A) `isAuthenticated` y `isAdmin`
    B) `appName` y `defaultImage`
    C) `cartItemCount` y `cartTotal`
    D) `csrfToken` y `csrfParamName`

19. ¿Cuál es la variable global de tipo `boolean` que se utiliza en las plantillas Pebble para verificar si el usuario autenticado posee el rol ADMIN?
    A) `userRole`
    B) `hasRoleAdmin`
    C) `isAdmin`
    D) `isAuthenticated`

20. ¿Cuál es una de las principales *malas prácticas* que puede llevar a un "Performance lento" si se realiza dentro de un método `@ModelAttribute` de `GlobalControllerAdvice`?
    A) Devolver un String con el nombre de la vista
    B) Usar `Lazy Loading` cuando sea posible
    C) Realizar *Queries pesadas a la base de datos* o cálculos complejos
    D) Documentar las variables globales

21. ¿Qué variable global de tipo `int` representa el número total de productos (cantidad de ítems) que hay en el carrito de compras?
    A) `cartTotal`
    B) `hasCartItems`
    C) `items_carrito`
    D) `cartItemCount`

22. Si un desarrollador necesita acceder al nombre de la aplicación desde una plantilla Pebble, ¿cuál es la variable global disponible?
    A) `username`
    B) `filesPath`
    C) `appName`
    D) `defaultImage`

23. ¿Cuál es la variable de Configuración Global que proporciona la ruta base para acceder a los archivos subidos (uploads)?
    A) `defaultImage`
    B) `currentDateTime`
    C) `filesPath`
    D) `csrfToken`

24. ¿Por qué la validación de formularios en el servidor (Bean Validation) se considera la única barrera de seguridad real?
    A) Porque JavaScript no puede usar expresiones regulares
    B) Porque la validación de servidor siempre es más rápida
    C) Porque Pebble requiere validación de servidor
    D) Porque un usuario malintencionado puede saltarse fácilmente la validación del cliente

25. ¿Cuál de los siguientes tipos de datos **NO** se recomienda inyectar mediante `GlobalControllerAdvice`?
    A) Tokens CSRF
    B) Información de autenticación
    C) Datos del carrito
    D) Queries pesadas a la base de datos o datos específicos de una sola vista

### III. Pebble Template Engine

26. En la sintaxis de Pebble, ¿qué delimitador se utiliza para ejecutar lógica de presentación, como condicionales (`if`) o bucles (`for`)?
    A) `{# ... #}`
    B) `<!-- ... -->`
    C) `{% ... %}`
    D) `{{ ... }}`

27. ¿Qué delimitador de Pebble se usa para imprimir o mostrar el contenido de una variable en la vista?
    A) `{% ... %}`
    B) `{# ... #}`
    C) `( ... )`
    D) `{{ ... }}`

28. ¿Qué medida de seguridad automática implementa Pebble por defecto al imprimir variables con `{{ ... }}` para prevenir ataques Cross-Site Scripting (XSS)?
    A) Protección CSRF
    B) Bean Validation
    C) Auto-escape de HTML
    D) Encoding de URL

29. El delimitador de comentarios de Pebble (`{# ... #}`) se caracteriza por:
    A) Ser un comentario HTML visible en el código fuente
    B) Ser eliminado completamente durante la compilación y no enviarse al navegador
    C) Usarse solo para depuración en producción
    D) Generar código condicional

30. ¿Cómo se llama el mecanismo de Pebble que permite definir un "esqueleto" base (`layouts/base.peb`) con "agujeros" (`block`) que las plantillas hijas rellenan?
    A) Includes
    B) Macros
    C) Internacionalización
    D) Herencia de Plantillas (extends)

31. Si en Pebble se utiliza un bucle `{% for item in collection %}` y la colección está vacía, ¿qué directiva permite mostrar un mensaje alternativo al usuario?
    A) `{% if collection is empty %}`
    B) `{% not in %}`
    C) `{% then %}`
    D) `{% else %}`

32. Dentro de un bucle `for` en Pebble, ¿cuál de las variables especiales devuelve el índice actual de la iteración comenzando en 1?
    A) `loop.index0`
    B) `loop.first`
    C) `loop.length`
    D) `loop.index`

33. ¿Cuál es la característica principal del filtro personalizado `formatPrice` implementado en el proyecto?
    A) Formatea fechas en formato español legible
    B) Elimina etiquetas HTML para seguridad
    C) Formatea números sin incluir el símbolo de moneda
    D) Formatea números como precios incluyendo el símbolo € y usando punto/coma como separadores

34. ¿Cuál es el operador que se utiliza en Pebble para concatenar (unir) dos cadenas de texto?
    A) `+`
    B) `&`
    C) `**`
    D) `~`

35. ¿Qué filtro de Pebble se utiliza para proporcionar un valor alternativo (por ejemplo, una imagen por defecto) si una variable es `null`, un String vacío o una colección vacía?
    A) `trim`
    B) `raw`
    C) `join`
    D) `default`

36. Si un desarrollador necesita insertar un fragmento de plantilla (como un navbar o un footer) dentro de otra plantilla, ¿qué directiva de Pebble usaría?
    A) `{% extends ... %}`
    B) `{% block ... %}`
    C) `{% macro ... %}`
    D) `{% include ... %}`

37. Las Macros en Pebble son principalmente utilizadas para:
    A) Transformar un valor de variable (ej. `|upper`)
    B) Generar datos nuevos (ej. `range(1, 10)`)
    C) Generar funciones reutilizables que devuelven HTML (ej. campos de formulario)
    D) Definir variables temporales con la directiva `set`

38. Según la filosofía de Pebble, ¿qué principio debe seguirse respecto a la lógica de negocio?
    A) Usar filtros complejos para transformaciones pesadas
    B) La lógica de negocio compleja y las operaciones de base de datos deben estar en el Controller/Service
    C) Usar la directiva `set` para cálculos complejos
    D) Realizar operaciones de hashing (sha1, md5) en la vista

39. ¿Cuál de los siguientes filtros comunes en otros motores de plantillas **NO** existe de forma nativa en Pebble, requiriendo un condicional o internacionalización?
    A) `slice`
    B) `upper`
    C) `date`
    D) `pluralize`

40. Si se necesita eliminar etiquetas HTML de una cadena (función `striptags`), Pebble recomienda realizar esta acción:
    A) Usando el filtro `raw`
    B) En el Controller/Service usando una librería como Jsoup
    C) Usando la directiva `set`
    D) Configurando el auto-escape

### IV. Estado, Seguridad y Formularios

41. ¿Cuál es el requisito fundamental que deben cumplir *todos* los formularios que envían peticiones POST, PUT o DELETE para no ser rechazados por Spring Security con un Error 403 Forbidden?
    A) Deben usar un DTO (Data Transfer Object)
    B) Deben devolver una redirección (PRG)
    C) Deben usar la anotación `@Valid`
    D) Deben incluir el token CSRF (Cross-Site Request Forgery) en un campo oculto

42. En el mecanismo de Sesión HTTP, ¿dónde se almacena el "almacén" de datos temporal asociado a un usuario único?
    A) En una cookie en el navegador del cliente
    B) En el servidor (gestionado por Spring)
    C) En la base de datos (PostgreSQL)
    D) En el objeto Model

43. ¿Qué anotación se utiliza en un parámetro de método del Controller para LEER un atributo de sesión *existente* (como el carrito de compras)?
    A) `@ModelAttribute`
    B) `@SessionAttributes` (a nivel de clase)
    C) `@Autowired`
    D) `@SessionAttribute`

44. ¿Qué librería se integra con Spring Boot y utiliza anotaciones como `@NotEmpty` o `@Min` para aplicar reglas de validación estricta en el servidor?
    A) Spring Security
    B) Jsoup
    C) Bean Validation (Hibernate Validator)
    D) MockMvc

45. Para activar la validación de un formulario en un método POST del Controller, ¿qué dos parámetros deben incluirse *inmediatamente* después del `@ModelAttribute` (DTO/Entidad) para capturar los errores?
    A) `Model` y `RedirectAttributes`
    B) `HttpSession` y `Principal`
    C) `Pageable` y `Page`
    D) `@Valid` y `BindingResult`

46. ¿Qué interfaz de Spring Data JPA representa una colección de datos paginada e incluye metadatos como el número total de elementos y páginas?
    A) `Slice`
    B) `Pageable`
    C) `List`
    D) `Page`

47. El principal problema de rendimiento al usar la interfaz `Page<T>` en repositorios grandes es que siempre ejecuta:
    A) Una consulta JOIN compleja
    B) Una consulta extra de conteo (`SELECT COUNT(*)`) que puede ser muy lenta
    C) Un filtro de seguridad CSRF
    D) Un ciclo de bucle infinito en Pebble

48. ¿Cuál es un caso de uso común y apropiado para almacenar datos en *Cookies* (que se guardan en el navegador del cliente)?
    A) Almacenar contraseñas o roles de usuario
    B) Almacenar objetos Java complejos (ej. el Carrito)
    C) Recordar preferencias de usuario, como el idioma (Internacionalización)
    D) Almacenar el token CSRF secreto

49. Si una variable global (`cartItemCount`) no aparece en la vista (Troubleshooting), ¿qué se debe verificar en el `GlobalControllerAdvice`?
    A) Que el método use `@GetMapping`
    B) Que se esté usando `ModelAndView` en lugar de `Model`
    C) Que el método esté anotado con `@ModelAttribute` y la clase con `@ControllerAdvice`
    D) Que la lógica de negocio esté en el Controller

50. ¿Qué patrón de comunicación se utiliza cuando JavaScript (AJAX/Fetch) envía una petición al servidor y el servidor responde *solo con los datos necesarios* en formato JSON (sin recargar la página)?
    A) Herencia de plantillas (Pebble)
    B) Patrón Post-Redirect-Get (PRG)
    C) API REST (usando @RestController)
    D) El patrón Service Layer