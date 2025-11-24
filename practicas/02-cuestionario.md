### 10 Preguntas de Investigación y Desarrollo (R&D)

1. **Optimización del Rendimiento en `GlobalControllerAdvice`:**
    Las variables en `GlobalControllerAdvice` se calculan en **cada petición HTTP**. Discuta detalladamente cómo la implementación de *Queries pesadas a la base de datos* o *Cálculos complejos* dentro de un método `@ModelAttribute` puede llevar al problema de **Performance lento**. Proponga y justifique al menos tres estrategias de optimización recomendadas (como *Cachear*, *Usar sesión*, o *Lazy Loading*) que el proyecto debe aplicar para mitigar este riesgo.

2. **Decisión Arquitectónica: `Model` vs. `ModelAndView`:**
    Aunque ambos se usan para pasar datos a la vista, las fuentes recomiendan usar `Model` **por defecto** para el 95% de los casos. Investigue y contraste las características que hacen a `Model` el *enfoque moderno, más limpio y flexible* frente a `ModelAndView`. ¿Cuáles son los **casos especiales** (mencionados en las fuentes) donde `ModelAndView` aún podría justificarse, particularmente en relación con el control sobre la respuesta HTTP?.

3. **Filosofía del Motor de Plantillas y la Lógica:**
    Pebble sigue estrictamente el principio de **"Lógica en el Controller, Presentación en la Vista"**. Analice por qué filtros de funcionalidad común como `striptags` (Eliminar HTML) o `pluralize` (Pluralización) **NO existen** de forma nativa en Pebble. Explique dónde y cómo el desarrollador debe implementar la lógica subyacente (ej. usando una librería como Jsoup o usando internacionalización) para mantener la filosofía de Pebble.

4. **El Patrón Post-Redirect-Get (PRG) y los `RedirectAttributes`:**
    El Patrón PRG es una **buena práctica obligatoria** después de procesar formularios POST. Explique el riesgo de seguridad/usabilidad que intenta prevenir el patrón PRG (el reenvío accidental del formulario). Luego, detalle cómo los `RedirectAttributes` resuelven el problema inherente a las redirecciones (la pérdida del `Model`) y cómo el uso de *Flash Attributes* difiere del simple paso de datos mediante el `Model` estándar.

5. **Seguridad CSRF en Diferentes Peticiones:**
    Spring Security protege contra la Falsificación de Peticiones en Sitios Cruzados (CSRF) exigiendo un token en **todos** los formularios POST, PUT y DELETE. Compare dos patrones para inyectar este token en la vista:
    1. Usando `@ControllerAdvice`.
    2. Usando JavaScript/AJAX para peticiones REST (vía meta tags).
    Justifique por qué el patrón de `GlobalControllerAdvice` se considera más **elegante y DRY** (Don't Repeat Yourself) para las vistas que devuelven HTML.

6. **Optimización de Paginación en Grandes Conjuntos de Datos:**
    Cuando se implementa paginación con Spring Data JPA, usar la interfaz `Page<T>` puede generar un cuello de botella en rendimiento para grandes repositorios. Explique la causa específica de esta lentitud (relacionada con una consulta de conteo SQL). Proponga la interfaz alternativa (`Slice<T>`) que se puede usar en el Repositorio y Servicio para mitigar este problema de rendimiento, indicando en qué tipo de interfaces de usuario (como "Cargar más") se recomienda su uso.

7. **Herencia de Plantillas vs. Inclusión de Fragmentos en Pebble:**
    Pebble ofrece dos mecanismos principales para la reutilización de código: Herencia (`extends`/`block`) e Inclusión (`include`). Analice la función arquitectónica de cada uno: ¿Cuál está diseñado para definir el **"esqueleto" o "layout"** base con "agujeros", y cuál se usa para componentes reutilizables y discretos, como un *navbar* o un *footer*?

8. **La Única Barrera de Seguridad: Validación en el Servidor:**
    La validación con JavaScript en el frontend es conveniente, pero se afirma que la **validación en el servidor** (usando **Bean Validation**) es la "única barrera de seguridad real". Argumente por qué un usuario malintencionado puede "saltársela fácilmente" en el cliente. Describa los dos parámetros **obligatorios** que deben seguir inmediatamente al `@ModelAttribute` en un método POST del Controller para que se active esta validación y se capturen los errores en el servidor (`BindingResult`).

9. **Patrón Service Layer y Controller Delgado:**
    El `Service Layer` se describe como el **"corazón" de la lógica de negocio** y el orquestador de los repositorios. Utilizando el *Flujo de la Lógica de Negocio* y el principio de **"Controlador delgado"**, demuestre, con un ejemplo conceptual, la diferencia entre la *mala práctica* de incluir lógica de negocio en el Controller (consultar BBDD directamente) y la *buena práctica* de delegar esa responsabilidad completamente al Service.

10. **Impacto de las Sesiones y las Cookies en la Seguridad:**
    Contraste los dos mecanismos de estado principales: Sesiones HTTP y Cookies. Basándose en la ubicación de almacenamiento de los datos (servidor vs. cliente), discuta las implicaciones de seguridad y justifique por qué las fuentes enfatizan que **nunca** se debe almacenar información sensible (como ID de usuario o rol) en una *cookie*, mientras que la `Sesión` se considera segura para almacenar objetos Java complejos como el carrito de compras.