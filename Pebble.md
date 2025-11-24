# Tutorial Exhaustivo de Pebble Template Engine

- [Tutorial Exhaustivo de Pebble Template Engine](#tutorial-exhaustivo-de-pebble-template-engine)
  - [Tabla de Contenidos](#tabla-de-contenidos)
  - [Introducción](#introducción)
    - [¿Por qué Pebble?](#por-qué-pebble)
    - [Pebble vs Thymeleaf](#pebble-vs-thymeleaf)
  - [Configuración](#configuración)
    - [Dependencias Gradle](#dependencias-gradle)
    - [application.properties](#applicationproperties)
    - [Estructura de Plantillas](#estructura-de-plantillas)
  - [Sintaxis Básica](#sintaxis-básica)
    - [Delimitadores](#delimitadores)
    - [Comentarios](#comentarios)
  - [Variables y Expresiones](#variables-y-expresiones)
    - [Acceso a Variables](#acceso-a-variables)
    - [Valores por Defecto](#valores-por-defecto)
    - [Operadores](#operadores)
      - [Aritméticos](#aritméticos)
      - [Comparación](#comparación)
      - [Lógicos](#lógicos)
      - [Ternario](#ternario)
    - [Concatenación](#concatenación)
  - [Estructuras de Control](#estructuras-de-control)
    - [Condicionales - if/elseif/else](#condicionales---ifelseifelse)
    - [Bucles - for](#bucles---for)
      - [Iteración Básica](#iteración-básica)
      - [Con Índice](#con-índice)
      - [Variables del Loop](#variables-del-loop)
      - [Lista Vacía](#lista-vacía)
      - [Iteración con Filtro](#iteración-con-filtro)
    - [Set - Asignar Variables](#set---asignar-variables)
  - [Filtros](#filtros)
    - [Filtros de Texto](#filtros-de-texto)
    - [Filtros Numéricos](#filtros-numéricos)
    - [Filtros de Fecha](#filtros-de-fecha)
    - [Filtros de Colecciones](#filtros-de-colecciones)
    - [Filtros de Escape](#filtros-de-escape)
    - [Filtros Condicionales](#filtros-condicionales)
    - [Encadenar Filtros](#encadenar-filtros)
  - [Filtros Personalizados](#filtros-personalizados)
    - [Configuración de Filtros Personalizados](#configuración-de-filtros-personalizados)
    - [Uso de Filtros Personalizados](#uso-de-filtros-personalizados)
      - [formatPrice](#formatprice)
      - [formatDate](#formatdate)
    - [Creando Filtros Adicionales](#creando-filtros-adicionales)
      - [Ejemplo: Filtro para Números (formatNumber)](#ejemplo-filtro-para-números-formatnumber)
      - [Ejemplo: Filtro Truncate con Elipsis](#ejemplo-filtro-truncate-con-elipsis)
    - [Registrar Múltiples Filtros](#registrar-múltiples-filtros)
    - [Best Practices para Filtros Personalizados](#best-practices-para-filtros-personalizados)
      - [1. Manejo de Null](#1-manejo-de-null)
      - [2. Validación de Tipos](#2-validación-de-tipos)
      - [3. Parámetros Opcionales](#3-parámetros-opcionales)
      - [4. Documentación Clara](#4-documentación-clara)
      - [5. Nombres Descriptivos](#5-nombres-descriptivos)
    - [Filtros vs Funciones](#filtros-vs-funciones)
  - [Funciones](#funciones)
    - [Funciones Incorporadas](#funciones-incorporadas)
    - [Funciones Personalizadas (i18n)](#funciones-personalizadas-i18n)
  - [Herencia y Layouts](#herencia-y-layouts)
    - [Layout Base](#layout-base)
    - [Plantilla Hija](#plantilla-hija)
    - [Bloques Múltiples](#bloques-múltiples)
  - [Macros](#macros)
    - [Definir Macros](#definir-macros)
    - [Usar Macros](#usar-macros)
    - [Macro con Contenido](#macro-con-contenido)
  - [Includes](#includes)
    - [Include Simple](#include-simple)
    - [Include con Variables](#include-con-variables)
    - [Include Condicional](#include-condicional)
  - [Integración con Datos de Sesión en Plantillas](#integración-con-datos-de-sesión-en-plantillas)
    - [Mostrar Datos de Sesión desde el Controller](#mostrar-datos-de-sesión-desde-el-controller)
      - [En el Controller](#en-el-controller)
      - [En la Plantilla Pebble](#en-la-plantilla-pebble)
    - [Ejemplo Completo: Carrito de Compras con Sesión](#ejemplo-completo-carrito-de-compras-con-sesión)
      - [Controller](#controller)
      - [Plantilla: carrito/ver.peb](#plantilla-carritoverpeb)
    - [Mostrar Mensaje de Bienvenida con Datos de Sesión](#mostrar-mensaje-de-bienvenida-con-datos-de-sesión)
    - [Condicionales Basados en Datos de Sesión](#condicionales-basados-en-datos-de-sesión)
    - [Personalización de Vista Según Preferencias de Sesión](#personalización-de-vista-según-preferencias-de-sesión)
    - [Notificaciones y Mensajes Flash desde Sesión](#notificaciones-y-mensajes-flash-desde-sesión)
  - [Internacionalización](#internacionalización)
    - [Configuración](#configuración-1)
    - [Uso en Plantillas](#uso-en-plantillas)
    - [Selector de Idioma con Sesión](#selector-de-idioma-con-sesión)
  - [Best Practices](#best-practices)
    - [1. Estructura Organizada](#1-estructura-organizada)
    - [2. Naming Conventions](#2-naming-conventions)
    - [3. Separar Lógica de Presentación](#3-separar-lógica-de-presentación)
    - [4. Usar Macros para Componentes Repetitivos](#4-usar-macros-para-componentes-repetitivos)
    - [5. Escapar HTML por Defecto](#5-escapar-html-por-defecto)
    - [6. Comentar Plantillas Complejas](#6-comentar-plantillas-complejas)
    - [7. Usar Condicionales Simples](#7-usar-condicionales-simples)
  - [Recursos Adicionales](#recursos-adicionales)
  - [Casos de Uso Reales del Proyecto](#casos-de-uso-reales-del-proyecto)
    - [1. Verificación de Nulos con `is not null`](#1-verificación-de-nulos-con-is-not-null)
    - [2. CSRF Tokens en Formularios](#2-csrf-tokens-en-formularios)
    - [3. Rutas Dinámicas y Parámetros](#3-rutas-dinámicas-y-parámetros)
    - [4. Cálculos de IVA en Facturas](#4-cálculos-de-iva-en-facturas)
    - [5. Iteración con Filtro Condicional](#5-iteración-con-filtro-condicional)
    - [6. Estados Dinámicos con Íconos](#6-estados-dinámicos-con-íconos)
    - [7. Renderizado de Estrellas de Rating](#7-renderizado-de-estrellas-de-rating)
    - [8. Condicionales de Autenticación y Roles](#8-condicionales-de-autenticación-y-roles)
    - [9. Listas Vacías con Mensaje Alternativo](#9-listas-vacías-con-mensaje-alternativo)
    - [10. Includes de Fragments](#10-includes-de-fragments)
    - [11. Valores por Defecto en Formularios](#11-valores-por-defecto-en-formularios)
    - [12. Badges Condicionales con Clases Dinámicas](#12-badges-condicionales-con-clases-dinámicas)
    - [13. JavaScript Embebido con Datos de Pebble](#13-javascript-embebido-con-datos-de-pebble)
    - [14. Estilos Inline Dinámicos](#14-estilos-inline-dinámicos)
    - [15. Uso de Variables de Sesión y ModelAttributes](#15-uso-de-variables-de-sesión-y-modelattributes)
  - [Filtros Personalizados Implementados](#filtros-personalizados-implementados)
    - [formatPrice](#formatprice-1)
    - [formatDate](#formatdate-1)
    - [number\_format](#number_format)
  - [Errores Comunes y Soluciones](#errores-comunes-y-soluciones)
    - [Error: "Wrong operand(s) type in conditional expression"](#error-wrong-operands-type-in-conditional-expression)
    - [Error: "Invalid CSRF token"](#error-invalid-csrf-token)
    - [Error: Variable no encontrada](#error-variable-no-encontrada)
    - [Error: Ruta 404](#error-ruta-404)
  - [Filtros que NO Existen en Pebble y Soluciones Alternativas](#filtros-que-no-existen-en-pebble-y-soluciones-alternativas)
    - [❌ Filtros que NO Existen](#-filtros-que-no-existen)
      - [1. `truncate` o `truncatewords`](#1-truncate-o-truncatewords)
      - [2. `striptags` (Eliminar HTML)](#2-striptags-eliminar-html)
      - [3. `pluralize` (Pluralización)](#3-pluralize-pluralización)
      - [4. `currency` o `money`](#4-currency-o-money)
      - [5. `slugify` (Convertir a URL-friendly)](#5-slugify-convertir-a-url-friendly)
      - [6. `date` con zonas horarias](#6-date-con-zonas-horarias)
      - [7. `wordcount` (Contar palabras)](#7-wordcount-contar-palabras)
      - [8. `random` (Elemento aleatorio)](#8-random-elemento-aleatorio)
      - [9. `sha1`, `sha256`, `md5` (Hashing)](#9-sha1-sha256-md5-hashing)
      - [10. `default_if_none` (Similar a `default` pero solo para null)](#10-default_if_none-similar-a-default-pero-solo-para-null)
    - [Resumen de Alternativas](#resumen-de-alternativas)
    - [Filosofía de Pebble](#filosofía-de-pebble)
    - [Cuándo Crear Filtros Personalizados](#cuándo-crear-filtros-personalizados)
    - [Mejores Prácticas](#mejores-prácticas)
      - [1. Preparar Datos en el Controller](#1-preparar-datos-en-el-controller)
      - [2. Usar DTOs para Datos Complejos](#2-usar-dtos-para-datos-complejos)
      - [3. Documentar Filtros Personalizados](#3-documentar-filtros-personalizados)


## Tabla de Contenidos

- [Introducción](#introducción)
- [Configuración](#configuración)
- [Sintaxis Básica](#sintaxis-básica)
- [Variables y Expresiones](#variables-y-expresiones)
- [Estructuras de Control](#estructuras-de-control)
- [Filtros](#filtros)
- [Funciones](#funciones)
- [Herencia y Layouts](#herencia-y-layouts)
- [Macros](#macros)
- [Includes](#includes)
- [Internacionalización](#internacionalización)
- [Best Practices](#best-practices)

## Introducción

**Pebble** es un motor de plantillas Java inspirado en Twig (PHP) con características modernas, alto rendimiento y sintaxis limpia.

### ¿Por qué Pebble?

✅ **Rápido**: Compilación automática de plantillas  
✅ **Seguro**: Auto-escaping para prevenir XSS  
✅ **Flexible**: Herencia, macros, filtros personalizados  
✅ **Legible**: Sintaxis clara y concisa  
✅ **Moderno**: Integración perfecta con Spring Boot  

### Pebble vs Thymeleaf

| Característica | Pebble | Thymeleaf |
|----------------|--------|-----------|
| **Sintaxis** | `{{ variable }}` | `th:text="${variable}"` |
| **Rendimiento** | Más rápido | Más lento |
| **Curva de aprendizaje** | Baja | Media |
| **Natural templates** | No | Sí |
| **Herencia** | Sí (simple) | Sí (complicada) |

## Configuración

### Dependencias Gradle

```kotlin
dependencies {
    implementation("io.pebbletemplates:pebble-spring-boot-starter:3.2.2")
    implementation("io.pebbletemplates:pebble:3.2.2")
}
```

### application.properties

```properties
# Configuración de Pebble
pebble.cache=false                    # Desactivar cache en desarrollo
pebble.suffix=.peb                    # Extensión de archivos
pebble.defaultLocale=es_ES            # Idioma por defecto
```

### Estructura de Plantillas

```
src/main/resources/templates/
├── fragments/          # Componentes reutilizables
│   ├── head.peb
│   ├── navbar.peb
│   └── footer.peb
├── layouts/            # Layouts base
│   └── base.peb
├── productos/          # Plantillas de productos
│   ├── lista.peb
│   ├── detalle.peb
│   └── form.peb
└── index.peb          # Página principal
```

## Sintaxis Básica

### Delimitadores

Pebble utiliza tres tipos de delimitadores:

```twig
{# Comentarios - No se renderizan #}
{# Esto es un comentario que no aparece en el HTML final #}

{{ expresión }}
{# Salida de variables - Se renderiza y se escapa automáticamente #}
{{ producto.nombre }}
{{ usuario.email }}

{% etiqueta %}
{# Etiquetas de control - if, for, block, etc. #}
{% if usuario %}
    <p>Bienvenido</p>
{% endif %}
```

### Comentarios

```twig
{# Comentario de una línea #}

{#
    Comentario
    multilínea
    para documentar
#}
```

## Variables y Expresiones

### Acceso a Variables

```twig
{# Variable simple #}
{{ nombre }}

{# Propiedad de objeto #}
{{ producto.nombre }}
{{ usuario.email }}

{# Método getter #}
{{ producto.getPrecio() }}
{{ usuario.getNombre() }}

{# Acceso a array/lista #}
{{ productos[0] }}
{{ productos[indice] }}

{# Acceso a map #}
{{ datos['clave'] }}
{{ datos.clave }}
```

### Valores por Defecto

```twig
{# Si la variable no existe, usar valor por defecto #}
{{ nombre | default('Anónimo') }}
{{ precio | default(0) }}
{{ descripcion | default('Sin descripción') }}
```

### Operadores

#### Aritméticos

```twig
{{ 5 + 3 }}        {# 8 #}
{{ 10 - 4 }}       {# 6 #}
{{ 6 * 7 }}        {# 42 #}
{{ 15 / 3 }}       {# 5 #}
{{ 17 % 5 }}       {# 2 (módulo) #}
```

#### Comparación

```twig
{{ precio > 100 }}
{{ edad >= 18 }}
{{ nombre == 'Admin' }}
{{ estado != 'inactivo' }}
{{ precio < 50 }}
{{ cantidad <= 10 }}
```

#### Lógicos

```twig
{{ true and false }}        {# false #}
{{ true or false }}         {# true #}
{{ not true }}              {# false #}
{{ (precio > 50) and (stock > 0) }}
```

#### Ternario

```twig
{{ edad >= 18 ? 'Adulto' : 'Menor' }}
{{ stock > 0 ? 'Disponible' : 'Agotado' }}
```

### Concatenación

```twig
{# Concatenar strings #}
{{ 'Hola ' ~ nombre ~ '!' }}
{{ 'Precio: ' ~ precio ~ '€' }}
```

## Estructuras de Control

### Condicionales - if/elseif/else

```twig
{% if usuario %}
    <p>Bienvenido, {{ usuario.nombre }}</p>
{% endif %}

{% if rol == 'ADMIN' %}
    <a href="/admin/dashboard">Panel Admin</a>
{% elseif rol == 'MODERATOR' %}
    <a href="/moderator/panel">Panel Moderador</a>
{% else %}
    <a href="/perfil">Mi Perfil</a>
{% endif %}

{# Operadores lógicos #}
{% if usuario and usuario.activo %}
    <p>Usuario activo</p>
{% endif %}

{% if precio > 100 or esOferta %}
    <span class="badge">Promoción</span>
{% endif %}
```

### Bucles - for

#### Iteración Básica

```twig
<ul>
{% for producto in productos %}
    <li>{{ producto.nombre }} - {{ producto.precio }}€</li>
{% endfor %}
</ul>
```

#### Con Índice

```twig
<table>
{% for producto in productos %}
    <tr>
        <td>{{ loop.index }}</td>      {# Índice desde 1 #}
        <td>{{ loop.index0 }}</td>     {# Índice desde 0 #}
        <td>{{ producto.nombre }}</td>
    </tr>
{% endfor %}
</table>
```

#### Variables del Loop

```twig
{% for item in items %}
    <div class="{{ loop.first ? 'primero' : '' }} {{ loop.last ? 'ultimo' : '' }}">
        <p>Item {{ loop.index }} de {{ loop.length }}</p>
        <p>{{ item.nombre }}</p>
    </div>
{% endfor %}

{# Propiedades disponibles:
   - loop.index: índice actual (desde 1)
   - loop.index0: índice actual (desde 0)
   - loop.revindex: índice invertido (desde length hasta 1)
   - loop.revindex0: índice invertido (desde length-1 hasta 0)
   - loop.first: true si es la primera iteración
   - loop.last: true si es la última iteración
   - loop.length: número total de items
#}
```

#### Lista Vacía

```twig
{% for producto in productos %}
    <div class="producto">{{ producto.nombre }}</div>
{% else %}
    <p>No hay productos disponibles</p>
{% endfor %}
```

#### Iteración con Filtro

```twig
{% for producto in productos if producto.precio < 100 %}
    <div>{{ producto.nombre }}</div>
{% endfor %}
```

### Set - Asignar Variables

```twig
{% set total = 0 %}
{% set nombre = 'Juan' %}
{% set precio = producto.precio * 1.21 %}

{# Asignación múltiple #}
{% set x, y, z = 1, 2, 3 %}
```

## Filtros

Los filtros transforman valores. Se aplican con el operador `|`:

### Filtros de Texto

```twig
{# Mayúsculas/Minúsculas #}
{{ 'hola mundo' | upper }}           {# HOLA MUNDO #}
{{ 'HOLA MUNDO' | lower }}           {# hola mundo #}
{{ 'hola mundo' | capitalize }}      {# Hola mundo #}
{{ 'hola mundo' | title }}           {# Hola Mundo #}

{# Trim - Eliminar espacios #}
{{ '  texto  ' | trim }}             {# texto #}

{# Truncar #}
{{ descripcion | slice(0, 100) }}    {# Primeros 100 caracteres #}
{{ texto | abbreviate(50) }}         {# Trunca a 50 y añade "..." #}

{# Reemplazar #}
{{ texto | replace({'viejo': 'nuevo'}) }}

{# URL encode #}
{{ 'Hola Mundo' | url_encode }}      {# Hola+Mundo #}
```

### Filtros Numéricos

```twig
{# Formato de números #}
{{ 1234.5678 | numberformat }}                    {# 1,234.57 #}
{{ precio | numberformat('0.00') }}               {# Formato personalizado #}

{# Redondear #}
{{ 3.7 | round }}                                 {# 4 #}
{{ 3.14159 | round(2) }}                          {# 3.14 #}

{# Absoluto #}
{{ -5 | abs }}                                    {# 5 #}
```

### Filtros de Fecha

```twig
{# Formato de fecha #}
{{ fechaCompra | date('dd/MM/yyyy') }}            {# 15/01/2025 #}
{{ fechaCompra | date('dd MMM yyyy HH:mm') }}     {# 15 Ene 2025 14:30 #}
{{ fechaCompra | date('full') }}                  {# Formato completo #}

{# Formatos disponibles:
   - short: 15/01/25
   - medium: 15-ene-2025
   - long: 15 de enero de 2025
   - full: lunes, 15 de enero de 2025
#}
```

### Filtros de Colecciones

```twig
{# Longitud #}
{{ productos | length }}                          {# Número de elementos #}

{# Slice - Subconjunto #}
{{ productos | slice(0, 5) }}                     {# Primeros 5 elementos #}
{{ productos | slice(5, 10) }}                    {# Elementos 5 a 10 #}

{# Ordenar #}
{{ productos | sort }}                            {# Orden natural #}
{{ productos | sort('precio') }}                  {# Por propiedad #}

{# Reverso #}
{{ productos | reverse }}

{# Unir #}
{{ tags | join(', ') }}                           {# tag1, tag2, tag3 #}

{# Primero y último #}
{{ productos | first }}
{{ productos | last }}
```

### Filtros de Escape

```twig
{# HTML escape (por defecto) #}
{{ '<script>alert("XSS")</script>' }}
{# Renderiza: &lt;script&gt;alert("XSS")&lt;/script&gt; #}

{# Sin escape (usar con cuidado) #}
{{ htmlContenido | raw }}

{# JSON #}
{{ objeto | json_encode }}

{# URL #}
{{ parametro | url_encode }}
```

### Filtros Condicionales

```twig
{# Default - Valor por defecto #}
{{ nombre | default('Anónimo') }}

{# Empty check #}
{% if productos is empty %}
    <p>No hay productos</p>
{% endif %}

{% if usuario is not empty %}
    <p>Hola, {{ usuario.nombre }}</p>
{% endif %}
```

### Encadenar Filtros

```twig
{{ producto.descripcion | trim | upper | slice(0, 50) }}
{{ precio | numberformat | default('Gratis') }}
{{ texto | lower | capitalize | abbreviate(100) }}
```

## Filtros Personalizados

Pebble permite crear filtros personalizados para necesidades específicas de la aplicación.

### Configuración de Filtros Personalizados

```java
package com.joseluisgs.walaspringboot.config;

import io.pebbletemplates.pebble.extension.AbstractExtension;
import io.pebbletemplates.pebble.extension.Filter;
import io.pebbletemplates.boot.autoconfigure.PebbleAutoConfiguration;
import org.springframework.boot.autoconfigure.AutoConfigureBefore;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.text.DecimalFormat;
import java.text.DecimalFormatSymbols;
import java.text.SimpleDateFormat;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Locale;
import java.util.Map;

@Configuration
@AutoConfigureBefore(PebbleAutoConfiguration.class)
public class PebbleConfig {

    @Bean
    public io.pebbletemplates.pebble.extension.Extension customPebbleExtension() {
        return new AbstractExtension() {
            @Override
            public Map<String, Filter> getFilters() {
                Map<String, Filter> filters = new HashMap<>();
                filters.put("formatDate", new FormatDateFilter());
                filters.put("formatPrice", new FormatPriceFilter());
                return filters;
            }
        };
    }

    // Filtro para formatear fechas
    private static class FormatDateFilter implements Filter {
        @Override
        public Object apply(Object input, Map<String, Object> args, 
                          io.pebbletemplates.pebble.template.PebbleTemplate self,
                          io.pebbletemplates.pebble.template.EvaluationContext context, 
                          int lineNumber) throws io.pebbletemplates.pebble.error.PebbleException {
            if (input == null) {
                return "";
            }

            try {
                DateTimeFormatter formatter = DateTimeFormatter.ofPattern(
                    "d MMM yyyy, HH:mm", 
                    new Locale("es", "ES")
                );
                
                if (input instanceof LocalDateTime) {
                    return ((LocalDateTime) input).format(formatter);
                } else if (input instanceof Date) {
                    SimpleDateFormat sdf = new SimpleDateFormat(
                        "d MMM yyyy, HH:mm", 
                        new Locale("es", "ES")
                    );
                    return sdf.format((Date) input);
                } else if (input instanceof String) {
                    // Try to parse as LocalDateTime
                    try {
                        LocalDateTime dateTime = LocalDateTime.parse(input.toString());
                        return dateTime.format(formatter);
                    } catch (Exception e) {
                        return input.toString();
                    }
                }
            } catch (Exception e) {
                return input.toString();
            }
            
            return input.toString();
        }

        @Override
        public List<String> getArgumentNames() {
            return null;
        }
    }

    // Filtro para formatear precios
    private static class FormatPriceFilter implements Filter {
        @Override
        public Object apply(Object input, Map<String, Object> args, 
                          io.pebbletemplates.pebble.template.PebbleTemplate self,
                          io.pebbletemplates.pebble.template.EvaluationContext context, 
                          int lineNumber) throws io.pebbletemplates.pebble.error.PebbleException {
            if (input == null) {
                return "0,00 €";
            }

            try {
                double price;
                if (input instanceof Number) {
                    price = ((Number) input).doubleValue();
                } else {
                    price = Double.parseDouble(input.toString());
                }

                DecimalFormatSymbols symbols = new DecimalFormatSymbols(new Locale("es", "ES"));
                symbols.setDecimalSeparator(',');
                symbols.setGroupingSeparator('.');
                
                DecimalFormat df = new DecimalFormat("#,##0.00 €", symbols);
                return df.format(price);
            } catch (Exception e) {
                return input.toString() + " €";
            }
        }

        @Override
        public List<String> getArgumentNames() {
            return null;
        }
    }
}
```

### Uso de Filtros Personalizados

#### formatPrice

Formatea números como precios con el símbolo € y separadores de miles y decimales según la localización española.

```twig
{# Precio simple #}
{{ 99.99 | formatPrice }}
{# Salida: 99,99 € #}

{# Precio con miles #}
{{ 1599.50 | formatPrice }}
{# Salida: 1.599,50 € #}

{# Variable de precio #}
<span class="badge bg-success">{{ producto.precio | formatPrice }}</span>

{# Total del carrito #}
<h4>Total: {{ total_carrito | formatPrice }}</h4>
```

**Características:**
- ✅ Separador de miles: punto (.)
- ✅ Separador de decimales: coma (,)
- ✅ Siempre muestra 2 decimales
- ✅ Añade símbolo € al final
- ✅ Maneja valores null como "0,00 €"

#### formatDate

Formatea fechas en formato español legible.

```twig
{# Fecha de compra #}
<span>Fecha: {{ compra.fechaCompra | formatDate }}</span>
{# Salida: 15 nov 2025, 14:30 #}

{# Fecha de registro #}
<small>Registrado: {{ usuario.fechaRegistro | formatDate }}</small>
{# Salida: 1 ene 2025, 09:15 #}

{# En tarjeta #}
<div class="card-header">
    <span>Compra #{{ compra.id }}</span>
    <span>{{ compra.fechaCompra | formatDate }}</span>
</div>
```

**Características:**
- ✅ Formato: "d MMM yyyy, HH:mm"
- ✅ Meses en español abreviados (ene, feb, mar...)
- ✅ Soporta LocalDateTime y Date
- ✅ Maneja valores null devolviendo string vacío

### Creando Filtros Adicionales

#### Ejemplo: Filtro para Números (formatNumber)

Si necesitas formatear números sin el símbolo €:

```java
private static class FormatNumberFilter implements Filter {
    @Override
    public Object apply(Object input, Map<String, Object> args, 
                      io.pebbletemplates.pebble.template.PebbleTemplate self,
                      io.pebbletemplates.pebble.template.EvaluationContext context, 
                      int lineNumber) throws io.pebbletemplates.pebble.error.PebbleException {
        if (input == null) {
            return "0";
        }

        try {
            // Obtener decimales del argumento (por defecto 0)
            int decimals = 0;
            if (args.containsKey("decimals")) {
                decimals = ((Number) args.get("decimals")).intValue();
            }
            
            double number;
            if (input instanceof Number) {
                number = ((Number) input).doubleValue();
            } else {
                number = Double.parseDouble(input.toString());
            }

            DecimalFormatSymbols symbols = new DecimalFormatSymbols(new Locale("es", "ES"));
            symbols.setDecimalSeparator(',');
            symbols.setGroupingSeparator('.');
            
            String pattern = decimals > 0 ? 
                "#,##0." + "0".repeat(decimals) : 
                "#,##0";
            
            DecimalFormat df = new DecimalFormat(pattern, symbols);
            return df.format(number);
        } catch (Exception e) {
            return input.toString();
        }
    }

    @Override
    public List<String> getArgumentNames() {
        return List.of("decimals");
    }
}
```

**Uso:**
```twig
{# Sin decimales #}
{{ cantidad | formatNumber }}
{# Salida: 1.500 #}

{# Con 1 decimal #}
{{ averageRating | formatNumber(decimals=1) }}
{# Salida: 4,5 #}

{# Con 2 decimales #}
{{ precio | formatNumber(decimals=2) }}
{# Salida: 99,95 #}
```

#### Ejemplo: Filtro Truncate con Elipsis

```java
private static class TruncateFilter implements Filter {
    @Override
    public Object apply(Object input, Map<String, Object> args, 
                      io.pebbletemplates.pebble.template.PebbleTemplate self,
                      io.pebbletemplates.pebble.template.EvaluationContext context, 
                      int lineNumber) throws io.pebbletemplates.pebble.error.PebbleException {
        if (input == null) {
            return "";
        }

        String text = input.toString();
        int length = 100; // Por defecto
        
        if (args.containsKey("length")) {
            length = ((Number) args.get("length")).intValue();
        }
        
        if (text.length() <= length) {
            return text;
        }
        
        return text.substring(0, length) + "...";
    }

    @Override
    public List<String> getArgumentNames() {
        return List.of("length");
    }
}
```

**Uso:**
```twig
{# Descripción truncada #}
<p>{{ producto.descripcion | truncate(60) }}</p>
{# Salida: "Este es un producto muy interesante que tiene muchas ca..." #}

{# Sin parámetros (usa 100 por defecto) #}
<p>{{ texto | truncate }}</p>
```

### Registrar Múltiples Filtros

Para añadir el nuevo filtro al `PebbleConfig`:

```java
@Bean
public io.pebbletemplates.pebble.extension.Extension customPebbleExtension() {
    return new AbstractExtension() {
        @Override
        public Map<String, Filter> getFilters() {
            Map<String, Filter> filters = new HashMap<>();
            filters.put("formatDate", new FormatDateFilter());
            filters.put("formatPrice", new FormatPriceFilter());
            filters.put("formatNumber", new FormatNumberFilter());  // Nuevo
            filters.put("truncate", new TruncateFilter());          // Nuevo
            return filters;
        }
    };
}
```

### Best Practices para Filtros Personalizados

#### 1. Manejo de Null
```java
if (input == null) {
    return ""; // o valor por defecto apropiado
}
```

#### 2. Validación de Tipos
```java
try {
    if (input instanceof Number) {
        // manejar número
    } else {
        // intentar parsear
    }
} catch (Exception e) {
    return input.toString(); // fallback seguro
}
```

#### 3. Parámetros Opcionales
```java
@Override
public List<String> getArgumentNames() {
    return List.of("param1", "param2"); // o null si no hay parámetros
}
```

#### 4. Documentación Clara
```twig
{# ✅ Bien documentado #}
{# Formato: formatDate(fecha) -> "15 nov 2025, 14:30" #}
{{ compra.fechaCompra | formatDate }}

{# ✅ Con parámetros #}
{# Formato: truncate(texto, length=100) #}
{{ descripcion | truncate(60) }}
```

#### 5. Nombres Descriptivos
```java
// ✅ Bueno
filters.put("formatPrice", new FormatPriceFilter());
filters.put("formatDate", new FormatDateFilter());

// ❌ Malo
filters.put("fp", new FormatPriceFilter());
filters.put("fd", new FormatDateFilter());
```

### Filtros vs Funciones

| Aspecto | Filtros | Funciones |
|---------|---------|-----------|
| **Sintaxis** | `{{ valor \| filtro }}` | `{{ funcion(valor) }}` |
| **Uso** | Transformar valores existentes | Generar nuevos valores |
| **Encadenado** | `{{ valor \| filtro1 \| filtro2 }}` | No natural |
| **Ejemplo** | `{{ precio \| formatPrice }}` | `{{ range(1, 10) }}` |

**Cuando usar filtros:**
- Transformar datos de salida (formato, escape)
- Operaciones sobre valores del modelo
- Presentación de datos

**Cuando usar funciones:**
- Generar datos nuevos
- Operaciones complejas
- Utilidades reutilizables

## Funciones

### Funciones Incorporadas

```twig
{# Range - Secuencia de números #}
{% for i in range(1, 10) %}
    <div>Item {{ i }}</div>
{% endfor %}

{# Min/Max #}
{{ min(10, 20, 5) }}                              {# 5 #}
{{ max(10, 20, 5) }}                              {# 20 #}

{# Parent - En herencia #}
{% block content %}
    {{ parent() }}
    {# Incluye el contenido del bloque padre #}
{% endblock %}
```

### Funciones Personalizadas (i18n)

```twig
{# Internacionalización #}
{{ i18n('producto.nombre') }}
{{ i18n('mensaje.bienvenida', usuario.nombre) }}
```

## Herencia y Layouts

### Layout Base

**templates/layouts/base.peb:**

```twig
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}WalaDaw{% endblock %}</title>
    
    {% block styles %}
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    {% endblock %}
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        {% block navbar %}
        {# Navbar por defecto #}
        {% endblock %}
    </nav>
    
    <main class="container mt-4">
        {% block content %}
        {# Contenido principal - debe ser sobrescrito #}
        {% endblock %}
    </main>
    
    <footer class="mt-5 py-3 bg-light">
        {% block footer %}
        <p class="text-center">&copy; 2025 WalaDaw</p>
        {% endblock %}
    </footer>
    
    {% block scripts %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    {% endblock %}
</body>
</html>
```

### Plantilla Hija

**templates/productos/lista.peb:**

```twig
{% extends "layouts/base.peb" %}

{% block title %}Lista de Productos - {{ parent() }}{% endblock %}

{% block content %}
<h1>Productos Disponibles</h1>

<div class="row">
    {% for producto in productos %}
    <div class="col-md-4 mb-3">
        <div class="card">
            <img src="{{ producto.imagen }}" class="card-img-top" alt="{{ producto.nombre }}">
            <div class="card-body">
                <h5 class="card-title">{{ producto.nombre }}</h5>
                <p class="card-text">{{ producto.descripcion | abbreviate(100) }}</p>
                <p class="text-primary"><strong>{{ producto.precio }}€</strong></p>
                <a href="/producto/{{ producto.id }}" class="btn btn-primary">Ver Detalle</a>
            </div>
        </div>
    </div>
    {% endfor %}
</div>
{% endblock %}

{% block scripts %}
{{ parent() }}
<script>
    console.log('Lista de productos cargada');
</script>
{% endblock %}
```

### Bloques Múltiples

```twig
{% extends "layouts/base.peb" %}

{% block title %}Mi Página{% endblock %}

{% block styles %}
{{ parent() }}
<link rel="stylesheet" href="/css/custom.css">
{% endblock %}

{% block content %}
<h1>Contenido Principal</h1>
{% endblock %}

{% block scripts %}
{{ parent() }}
<script src="/js/custom.js"></script>
{% endblock %}
```

## Macros

Las macros son funciones reutilizables que generan HTML.

### Definir Macros

**templates/macros/forms.peb:**

```twig
{# Macro para input de texto #}
{% macro input(name, label, value='', type='text', required=false) %}
<div class="mb-3">
    <label for="{{ name }}" class="form-label">{{ label }}</label>
    <input type="{{ type }}" 
           class="form-control" 
           id="{{ name }}" 
           name="{{ name }}" 
           value="{{ value }}"
           {% if required %}required{% endif %}>
</div>
{% endmacro %}

{# Macro para textarea #}
{% macro textarea(name, label, value='', rows=3) %}
<div class="mb-3">
    <label for="{{ name }}" class="form-label">{{ label }}</label>
    <textarea class="form-control" 
              id="{{ name }}" 
              name="{{ name }}" 
              rows="{{ rows }}">{{ value }}</textarea>
</div>
{% endmacro %}

{# Macro para botón #}
{% macro button(text, type='primary', submit=true) %}
<button type="{% if submit %}submit{% else %}button{% endif %}" 
        class="btn btn-{{ type }}">
    {{ text }}
</button>
{% endmacro %}
```

### Usar Macros

```twig
{% import "macros/forms.peb" %}

<form method="POST" action="/producto/guardar">
    {{ input('nombre', 'Nombre del Producto', producto.nombre, required=true) }}
    {{ input('precio', 'Precio', producto.precio, type='number') }}
    {{ textarea('descripcion', 'Descripción', producto.descripcion, rows=5) }}
    {{ button('Guardar Producto') }}
    {{ button('Cancelar', type='secondary', submit=false) }}
</form>
```

### Macro con Contenido

```twig
{% macro card(title) %}
<div class="card">
    <div class="card-header">
        <h5>{{ title }}</h5>
    </div>
    <div class="card-body">
        {{ caller() }}
    </div>
</div>
{% endmacro %}

{# Usar con contenido #}
{% call card('Mi Tarjeta') %}
    <p>Este es el contenido de la tarjeta</p>
    <button class="btn btn-primary">Acción</button>
{% endcall %}
```

## Includes

### Include Simple

**templates/fragments/alert.peb:**

```twig
{% if mensaje %}
<div class="alert alert-{{ tipo | default('info') }} alert-dismissible fade show">
    {{ mensaje }}
    <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
{% endif %}
```

**Usar:**

```twig
{% include "fragments/alert.peb" %}
```

### Include con Variables

```twig
{% include "fragments/alert.peb" with {"mensaje": "Operación exitosa", "tipo": "success"} %}
```

### Include Condicional

```twig
{% if usuario.esAdmin %}
    {% include "fragments/admin-menu.peb" %}
{% endif %}
```

## Integración con Datos de Sesión en Plantillas

Las sesiones HTTP permiten mantener información del usuario entre diferentes peticiones. En Pebble, puedes acceder a datos de sesión que el controller pasa al modelo.

### Mostrar Datos de Sesión desde el Controller

#### En el Controller

```java
@ControllerAdvice
public class GlobalControllerAdvice {
    
    @ModelAttribute("carritoCount")
    public int carritoCount(HttpSession session) {
        @SuppressWarnings("unchecked")
        Map<Long, ItemCarrito> carrito = 
            (Map<Long, ItemCarrito>) session.getAttribute("carrito");
        return carrito != null ? carrito.values().stream()
            .mapToInt(ItemCarrito::getCantidad).sum() : 0;
    }
    
    @ModelAttribute("preferenciaIdioma")
    public String preferenciaIdioma(HttpSession session) {
        String idioma = (String) session.getAttribute("idioma");
        return idioma != null ? idioma : "es";
    }
}
```

#### En la Plantilla Pebble

```twig
{# Navbar con contador de carrito desde sesión #}
<nav class="navbar navbar-expand-lg">
    <ul class="navbar-nav">
        <li class="nav-item">
            <a class="nav-link" href="/carrito">
                <i class="bi bi-cart"></i> Carrito
                {% if carritoCount > 0 %}
                <span class="badge bg-danger">{{ carritoCount }}</span>
                {% endif %}
            </a>
        </li>
    </ul>
    
    {# Selector de idioma basado en preferencia de sesión #}
    <div class="dropdown">
        <button class="btn btn-link">
            {% if preferenciaIdioma == 'es' %}
            🇪🇸 Español
            {% else %}
            🇬🇧 English
            {% endif %}
        </button>
        <ul class="dropdown-menu">
            <li><a href="?lang=es">🇪🇸 Español</a></li>
            <li><a href="?lang=en">🇬🇧 English</a></li>
        </ul>
    </div>
</nav>
```

### Ejemplo Completo: Carrito de Compras con Sesión

#### Controller

```java
@Controller
@RequestMapping("/carrito")
public class CarritoController {
    
    @GetMapping("/ver")
    public String verCarrito(HttpSession session, Model model) {
        @SuppressWarnings("unchecked")
        Map<Long, ItemCarrito> carrito = 
            (Map<Long, ItemCarrito>) session.getAttribute("carrito");
        
        if (carrito == null) {
            carrito = new HashMap<>();
        }
        
        List<ItemCarrito> items = new ArrayList<>(carrito.values());
        double total = items.stream()
            .mapToDouble(item -> item.getProducto().getPrecio() * item.getCantidad())
            .sum();
        
        model.addAttribute("items", items);
        model.addAttribute("total", total);
        model.addAttribute("isEmpty", items.isEmpty());
        
        return "carrito/ver";
    }
}
```

#### Plantilla: carrito/ver.peb

```twig
{% extends "layouts/base.peb" %}

{% block title %}Mi Carrito de Compras{% endblock %}

{% block content %}
<div class="container mt-4">
    <h1><i class="bi bi-cart-fill"></i> Mi Carrito</h1>
    
    {# Verificar si el carrito está vacío #}
    {% if isEmpty %}
    <div class="alert alert-info">
        <i class="bi bi-info-circle"></i>
        Tu carrito está vacío. 
        <a href="/productos" class="alert-link">Explorar productos</a>
    </div>
    {% else %}
    
    {# Tabla de productos en el carrito #}
    <div class="card">
        <div class="card-body">
            <table class="table">
                <thead>
                    <tr>
                        <th>Producto</th>
                        <th>Precio Unitario</th>
                        <th>Cantidad</th>
                        <th>Subtotal</th>
                        <th>Acciones</th>
                    </tr>
                </thead>
                <tbody>
                    {% for item in items %}
                    <tr>
                        <td>
                            <div class="d-flex align-items-center">
                                <img src="{{ item.producto.imagen }}" 
                                     width="60" 
                                     class="me-3 rounded">
                                <div>
                                    <strong>{{ item.producto.nombre }}</strong>
                                    <br>
                                    <small class="text-muted">
                                        {{ item.producto.categoria }}
                                    </small>
                                </div>
                            </div>
                        </td>
                        <td>{{ item.producto.precio | numberformat('0.00') }}€</td>
                        <td>
                            <form method="POST" 
                                  action="/carrito/actualizar/{{ item.producto.id }}" 
                                  class="d-flex align-items-center">
                                <input type="number" 
                                       name="cantidad" 
                                       value="{{ item.cantidad }}" 
                                       min="1" 
                                       max="99" 
                                       class="form-control form-control-sm me-2" 
                                       style="width: 70px;">
                                <button type="submit" 
                                        class="btn btn-sm btn-outline-primary">
                                    <i class="bi bi-arrow-repeat"></i>
                                </button>
                            </form>
                        </td>
                        <td>
                            <strong>{{ item.subtotal | numberformat('0.00') }}€</strong>
                        </td>
                        <td>
                            <a href="/carrito/eliminar/{{ item.producto.id }}" 
                               class="btn btn-sm btn-danger"
                               onclick="return confirm('¿Eliminar este producto?')">
                                <i class="bi bi-trash"></i>
                            </a>
                        </td>
                    </tr>
                    {% endfor %}
                </tbody>
            </table>
            
            {# Total del carrito #}
            <div class="row">
                <div class="col-md-6 offset-md-6">
                    <div class="card bg-light">
                        <div class="card-body">
                            <h5>Resumen del Pedido</h5>
                            <hr>
                            <div class="d-flex justify-content-between">
                                <span>Subtotal ({{ items | length }} items):</span>
                                <strong>{{ total | numberformat('0.00') }}€</strong>
                            </div>
                            <div class="d-flex justify-content-between">
                                <span>Envío:</span>
                                <strong>
                                    {% if total > 50 %}
                                    <span class="text-success">GRATIS</span>
                                    {% else %}
                                    {{ 5.99 | numberformat('0.00') }}€
                                    {% endif %}
                                </strong>
                            </div>
                            <hr>
                            <div class="d-flex justify-content-between">
                                <strong>Total:</strong>
                                <strong class="text-primary fs-4">
                                    {{ (total > 50 ? total : total + 5.99) | numberformat('0.00') }}€
                                </strong>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    {# Botones de acción #}
    <div class="d-flex justify-content-between mt-4">
        <a href="/productos" class="btn btn-secondary">
            <i class="bi bi-arrow-left"></i> Seguir Comprando
        </a>
        <div>
            <a href="/carrito/vaciar" 
               class="btn btn-warning me-2"
               onclick="return confirm('¿Vaciar todo el carrito?')">
                <i class="bi bi-trash"></i> Vaciar Carrito
            </a>
            <a href="/compra/finalizar" class="btn btn-success btn-lg">
                <i class="bi bi-check-circle"></i> Proceder al Pago
            </a>
        </div>
    </div>
    
    {% endif %}
</div>
{% endblock %}
```

### Mostrar Mensaje de Bienvenida con Datos de Sesión

```twig
{# Mostrar nombre de usuario desde sesión #}
{% if usuarioNombre %}
<div class="alert alert-info">
    👋 Bienvenido de nuevo, <strong>{{ usuarioNombre }}</strong>!
    <a href="/auth/logout" class="btn btn-sm btn-outline-secondary ms-3">
        Cerrar Sesión
    </a>
</div>
{% endif %}

{# Mostrar última visita #}
{% if ultimaVisita %}
<p class="text-muted">
    Última visita: {{ ultimaVisita | date('dd/MM/yyyy HH:mm') }}
</p>
{% endif %}
```

### Condicionales Basados en Datos de Sesión

```twig
{# Mostrar diferentes opciones según rol del usuario #}
{% if usuarioRol == 'ADMIN' %}
<div class="admin-panel">
    <h3>Panel de Administración</h3>
    <ul>
        <li><a href="/admin/usuarios">Gestionar Usuarios</a></li>
        <li><a href="/admin/productos">Gestionar Productos</a></li>
        <li><a href="/admin/estadisticas">Ver Estadísticas</a></li>
    </ul>
</div>
{% elseif usuarioRol == 'MODERATOR' %}
<div class="moderator-panel">
    <h3>Panel de Moderación</h3>
    <ul>
        <li><a href="/moderador/reportes">Ver Reportes</a></li>
        <li><a href="/moderador/comentarios">Moderar Comentarios</a></li>
    </ul>
</div>
{% else %}
<div class="user-panel">
    <h3>Mi Cuenta</h3>
    <ul>
        <li><a href="/perfil">Mi Perfil</a></li>
        <li><a href="/compras">Mis Compras</a></li>
        <li><a href="/productos/mis-productos">Mis Productos</a></li>
    </ul>
</div>
{% endif %}

{# Mostrar banner promocional solo si el usuario no lo ha cerrado #}
{% if not bannerCerrado %}
<div class="alert alert-warning alert-dismissible">
    <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
    <strong>¡Oferta especial!</strong> 20% de descuento en tu primera compra.
    <a href="/promociones">Ver ofertas</a>
</div>
{% endif %}
```

### Personalización de Vista Según Preferencias de Sesión

```twig
{# Tema oscuro/claro basado en preferencia de sesión #}
<body class="{% if temaOscuro %}theme-dark{% else %}theme-light{% endif %}">

{# Vista de lista vs cuadrícula según preferencia #}
{% if vistaPreferida == 'grid' %}
<div class="row row-cols-1 row-cols-md-3 g-4">
    {% for producto in productos %}
    <div class="col">
        <div class="card">
            <img src="{{ producto.imagen }}" class="card-img-top">
            <div class="card-body">
                <h5>{{ producto.nombre }}</h5>
                <p>{{ producto.precio }}€</p>
            </div>
        </div>
    </div>
    {% endfor %}
</div>
{% else %}
<div class="list-group">
    {% for producto in productos %}
    <div class="list-group-item">
        <div class="d-flex">
            <img src="{{ producto.imagen }}" width="100" class="me-3">
            <div>
                <h5>{{ producto.nombre }}</h5>
                <p>{{ producto.descripcion | slice(0, 100) }}...</p>
                <strong>{{ producto.precio }}€</strong>
            </div>
        </div>
    </div>
    {% endfor %}
</div>
{% endif %}

{# Botones para cambiar vista #}
<div class="btn-group mb-3">
    <a href="/productos?vista=grid" 
       class="btn btn-outline-secondary {{ vistaPreferida == 'grid' ? 'active' : '' }}">
        <i class="bi bi-grid-3x3"></i> Cuadrícula
    </a>
    <a href="/productos?vista=list" 
       class="btn btn-outline-secondary {{ vistaPreferida == 'list' ? 'active' : '' }}">
        <i class="bi bi-list"></i> Lista
    </a>
</div>
```

### Notificaciones y Mensajes Flash desde Sesión

```twig
{# Mostrar mensajes flash (almacenados temporalmente en sesión) #}
{% if mensaje %}
<div class="alert alert-success alert-dismissible fade show">
    <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
    <i class="bi bi-check-circle"></i> {{ mensaje }}
</div>
{% endif %}

{% if error %}
<div class="alert alert-danger alert-dismissible fade show">
    <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
    <i class="bi bi-exclamation-triangle"></i> {{ error }}
</div>
{% endif %}

{% if advertencia %}
<div class="alert alert-warning alert-dismissible fade show">
    <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
    <i class="bi bi-info-circle"></i> {{ advertencia }}
</div>
{% endif %}
```

## Internacionalización

### Configuración

**ConfiguracionI18n.java:**

```java
@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver slr = new SessionLocaleResolver();
    slr.setDefaultLocale(new Locale("es"));
    return slr;
}
```

**messages_es.properties:**

```properties
producto.nombre=Nombre del Producto
producto.precio=Precio
producto.crear=Crear Producto
usuario.bienvenida=Bienvenido, {0}
carrito.vacio=Tu carrito está vacío
carrito.items=items en el carrito
```

**messages_en.properties:**

```properties
producto.nombre=Product Name
producto.precio=Price
producto.crear=Create Product
usuario.bienvenida=Welcome, {0}
carrito.vacio=Your cart is empty
carrito.items=items in cart
```

### Uso en Plantillas

```twig
<h1>{{ i18n('producto.crear') }}</h1>

<label>{{ i18n('producto.nombre') }}</label>
<input type="text" name="nombre">

<label>{{ i18n('producto.precio') }}</label>
<input type="number" name="precio">

{# Con parámetros #}
<p>{{ i18n('usuario.bienvenida', usuario.nombre) }}</p>

{# En el carrito #}
{% if carritoCount > 0 %}
<span class="badge bg-primary">
    {{ carritoCount }} {{ i18n('carrito.items') }}
</span>
{% else %}
<p>{{ i18n('carrito.vacio') }}</p>
{% endif %}
```

### Selector de Idioma con Sesión

```twig
<div class="dropdown">
    <button class="btn btn-link dropdown-toggle" data-bs-toggle="dropdown">
        <i class="bi bi-globe"></i>
        {% if idiomaActual == 'es' %}
        Español
        {% else %}
        English
        {% endif %}
    </button>
    <ul class="dropdown-menu">
        <li>
            <a class="dropdown-item {{ idiomaActual == 'es' ? 'active' : '' }}" 
               href="?lang=es">
                🇪🇸 Español
            </a>
        </li>
        <li>
            <a class="dropdown-item {{ idiomaActual == 'en' ? 'active' : '' }}" 
               href="?lang=en">
                🇬🇧 English
            </a>
        </li>
    </ul>
</div>
```

## Best Practices

### 1. Estructura Organizada

```
templates/
├── layouts/           # Layouts base
├── fragments/         # Componentes pequeños
├── macros/           # Macros reutilizables
├── [modulo]/         # Por módulo (productos, usuarios, etc.)
└── errors/           # Páginas de error
```

### 2. Naming Conventions

```twig
{# Usar nombres descriptivos #}
{% block mainContent %}...{% endblock %}    ✅
{% block b1 %}...{% endblock %}             ❌

{# Variables en camelCase #}
{{ userName }}                              ✅
{{ user_name }}                             ❌
```

### 3. Separar Lógica de Presentación

❌ **Mal:**

```twig
{% set total = 0 %}
{% for item in carrito %}
    {% set total = total + (item.precio * item.cantidad) %}
{% endfor %}
{{ total }}
```

✅ **Bien:**

```java
// En el Controller
model.addAttribute("total", carritoServicio.calcularTotal());
```

```twig
{{ total }}
```

### 4. Usar Macros para Componentes Repetitivos

✅ **Bien:**

```twig
{% import "macros/cards.peb" %}

{% for producto in productos %}
    {{ productoCard(producto) }}
{% endfor %}
```

### 5. Escapar HTML por Defecto

```twig
{# Auto-escapado - Seguro #}
{{ comentario }}                            ✅

{# Raw - Solo si confías en el contenido #}
{{ htmlSeguro | raw }}                      ⚠️
```

### 6. Comentar Plantillas Complejas

```twig
{#
    Tarjeta de producto con:
    - Imagen
    - Nombre y descripción
    - Precio
    - Botón de compra
#}
<div class="producto-card">
    ...
</div>
```

### 7. Usar Condicionales Simples

❌ **Mal:**

```twig
{% if usuario %}
    {% if usuario.rol == 'ADMIN' %}
        {% if usuario.activo %}
            <a href="/admin">Panel</a>
        {% endif %}
    {% endif %}
{% endif %}
```

✅ **Bien:**

```twig
{% if usuario and usuario.rol == 'ADMIN' and usuario.activo %}
    <a href="/admin">Panel</a>
{% endif %}
```

## Recursos Adicionales

- [Pebble Documentation](https://pebbletemplates.io/)
- [Pebble GitHub](https://github.com/PebbleTemplates/pebble)
- [Spring Boot + Pebble](https://github.com/PebbleTemplates/pebble-spring-boot-starter)

---

**Última actualización:** Enero 2025  
**Autor:** José Luis González Sánchez

## Casos de Uso Reales del Proyecto

### 1. Verificación de Nulos con `is not null`

❌ **Problema:** Comparar directamente objetos causa PebbleException

```twig
{% if producto.compra %}  {# ERROR: Wrong operand type #}
    <span>Vendido</span>
{% endif %}
```

✅ **Solución:** Usar `is not null` para verificar objetos

```twig
{% if producto.compra is not null %}
    <span class="badge bg-success">Vendido</span>
{% else %}
    <span class="badge bg-warning">Disponible</span>
{% endif %}
```

### 2. CSRF Tokens en Formularios

```twig
<form method="post" action="/app/misproductos/editar/submit">
    {# IMPORTANTE: Incluir token CSRF para evitar error 403 #}
    <input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}"/>
    
    <input type="text" name="nombre" value="{{ producto.nombre | default('') }}">
    <button type="submit">Guardar</button>
</form>
```

### 3. Rutas Dinámicas y Parámetros

```twig
{# Factura con ID dinámico #}
<a href="/app/miscompras/factura/{{ compra.id }}" class="btn btn-primary">
    Ver Factura #{{ compra.id }}
</a>

{# PDF con ruta correcta #}
<a href="/app/miscompras/factura/{{ compra.id }}/pdf" class="btn btn-danger">
    <i class="bi bi-file-pdf"></i> Descargar PDF
</a>
```

### 4. Cálculos de IVA en Facturas

```twig
<table class="table">
    <tr>
        <td>Subtotal (sin IVA):</td>
        <td>{{ (total / 1.21) | formatPrice }}</td>
    </tr>
    <tr>
        <td>IVA (21%):</td>
        <td>{{ (total - (total / 1.21)) | formatPrice }}</td>
    </tr>
    <tr>
        <td><strong>TOTAL:</strong></td>
        <td><strong>{{ total | formatPrice }}</strong></td>
    </tr>
</table>
```

### 5. Iteración con Filtro Condicional

```twig
{# Mostrar solo productos de una compra específica #}
{% for producto in productos %}
    {% if producto.compra.id == compra.id %}
    <li class="list-group-item">
        <span>{{ producto.nombre }}</span>
        <span class="badge">{{ producto.precio | formatPrice }}</span>
    </li>
    {% endif %}
{% endfor %}
```

### 6. Estados Dinámicos con Íconos

```twig
{# Sistema de favoritos con estado dinámico #}
<button onclick="toggleFavorite({{ producto.id }})">
    <i class="bi bi-heart{% if isFavorite %}-fill{% endif %}" id="favoriteIcon"></i>
    <span id="favoriteText">
        {% if isFavorite %}Quitar de favoritos{% else %}Añadir a favoritos{% endif %}
    </span>
</button>
```

### 7. Renderizado de Estrellas de Rating

```twig
{# Mostrar rating promedio con estrellas #}
<div class="rating">
    {% if averageRating > 0 %}
    <div class="text-warning">
        {% for i in range(1, 6) %}
            {% if i <= averageRating %}
            <i class="bi bi-star-fill"></i>
            {% elseif i - averageRating < 1 %}
            <i class="bi bi-star-half"></i>
            {% else %}
            <i class="bi bi-star"></i>
            {% endif %}
        {% endfor %}
    </div>
    <span>{{ averageRating | number_format(1) }} ({{ ratingCount }} valoraciones)</span>
    {% else %}
    <span class="text-muted">Sin valoraciones</span>
    {% endif %}
</div>
```

### 8. Condicionales de Autenticación y Roles

```twig
{# Mostrar opciones según autenticación y rol #}
{% if isAuthenticated %}
    {% if currentUser.email != producto.propietario.email %}
        <a href="/app/carrito/add/{{ producto.id }}" class="btn btn-success">
            <i class="bi bi-cart-plus"></i> Comprar
        </a>
    {% endif %}
    
    {% if isAdmin %}
        <a href="/admin/productos/eliminar/{{ producto.id }}" class="btn btn-danger">
            Eliminar
        </a>
    {% endif %}
{% else %}
    <a href="/auth/login" class="btn btn-primary">
        Inicia sesión para comprar
    </a>
{% endif %}
```

### 9. Listas Vacías con Mensaje Alternativo

```twig
{# Mis compras con mensaje si está vacío #}
{% if miscompras is empty %}
<div class="alert alert-info">
    <p>No has realizado ninguna compra todavía.</p>
    <a href="/" class="btn btn-primary">Ir a comprar</a>
</div>
{% else %}
<div class="row">
    {% for compra in miscompras %}
    <div class="card">
        <h5>Compra #{{ compra.id }}</h5>
        <p>Fecha: {{ compra.fechaCompra | formatDate }}</p>
    </div>
    {% endfor %}
</div>
{% endif %}
```

### 10. Includes de Fragments

```twig
<!DOCTYPE html>
<html lang="es">
{# Incluir head común #}
{% include "fragments/head" %}

<body>
    {# Incluir navbar #}
    {% include "fragments/navbar" %}
    
    <main>
        {# Contenido específico de la página #}
    </main>
    
    {# Incluir footer #}
    {% include "fragments/footer" %}
</body>
</html>
```

### 11. Valores por Defecto en Formularios

```twig
{# Formulario que funciona para crear Y editar #}
<form method="post" action="{% if producto.id != 0 %}/editar/submit{% else %}/nuevo/submit{% endif %}">
    <input type="hidden" name="id" value="{{ producto.id | default(0) }}">
    
    <input type="text" 
           name="nombre" 
           value="{{ producto.nombre | default('') }}" 
           required>
    
    <input type="number" 
           step="0.01" 
           name="precio" 
           value="{{ producto.precio | default(0) }}" 
           min="0.01" 
           required>
    
    <button type="submit">
        {% if producto.id != 0 %}Actualizar{% else %}Crear{% endif %}
    </button>
</form>
```

### 12. Badges Condicionales con Clases Dinámicas

```twig
{# Badge que cambia de color según el estado #}
{% if producto.compra is not null %}
    <span class="badge bg-success">Vendido</span>
{% else %}
    <span class="badge bg-warning">Disponible</span>
{% endif %}

{# Badge de carrito con contador dinámico #}
<a href="/app/carrito">
    <span class="badge bg-danger">{{ items_carrito | default(0) }}</span>
    <i class="bi bi-cart"></i> Carrito
</a>
```

### 13. JavaScript Embebido con Datos de Pebble

```twig
<script>
// Cargar valoraciones al iniciar la página
{% if isAuthenticated %}
document.addEventListener('DOMContentLoaded', function() {
    loadRatings({{ producto.id }});
});
{% endif %}

// Función con parámetros desde Pebble
function toggleFavorite(productoId) {
    fetch(`/app/favoritos/add/${productoId}`, {
        method: 'POST'
    }).then(response => response.json())
      .then(data => console.log(data));
}
</script>
```

### 14. Estilos Inline Dinámicos

```twig
{# Barra de progreso según porcentaje #}
<div class="progress">
    <div class="progress-bar" 
         style="width: {{ porcentaje }}%"
         role="progressbar">
        {{ porcentaje }}%
    </div>
</div>

{# Imagen con fallback #}
<img src="{% if producto.imagen is empty %}https://placehold.it/300x200{% else %}{{ producto.imagen }}{% endif %}"
     alt="{{ producto.nombre }}"
     class="img-fluid">
```

### 15. Uso de Variables de Sesión y ModelAttributes

```twig
{# Variables inyectadas automáticamente por @ModelAttribute #}
<p>Total del carrito: {{ total_carrito | formatPrice }}</p>
<p>Items en carrito: {{ items_carrito }}</p>

{# Información del usuario autenticado (GlobalControllerAdvice) #}
<p>Bienvenido, {{ username | default('Usuario') }}</p>
<p>Rol: {{ userRole | default('USER') }}</p>

{# Variables de sesión #}
{% if session.getAttribute('mensaje') %}
<div class="alert alert-info">{{ session.getAttribute('mensaje') }}</div>
{% endif %}
```

## Filtros Personalizados Implementados

### formatPrice
```twig
{{ 99.99 | formatPrice }}  {# Salida: 99,99 € #}
{{ total | formatPrice }}   {# Formatea según locale #}
```

### formatDate
```twig
{{ compra.fechaCompra | formatDate }}  {# Salida: 15/01/2025 #}
```

### number_format
```twig
{{ averageRating | number_format(1) }}  {# Salida: 4.5 #}
{{ precio | number_format(2) }}         {# Salida: 99.95 #}
```

## Errores Comunes y Soluciones

### Error: "Wrong operand(s) type in conditional expression"
```twig
❌ {% if objeto %}           {# Error con objetos #}
✅ {% if objeto is not null %}  {# Correcto #}
```

### Error: "Invalid CSRF token"
```twig
❌ <form method="post">  {# Falta token #}
✅ <form method="post">
    <input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}"/>
</form>
```

### Error: Variable no encontrada
```twig
❌ {{ precio }}              {# Error si no existe #}
✅ {{ precio | default(0) }}  {# Con valor por defecto #}
```

### Error: Ruta 404
```twig
❌ <a href="/app/compra/factura/{{ id }}/pdf">  {# Ruta incorrecta #}
✅ <a href="/app/miscompras/factura/{{ id }}/pdf">  {# Ruta correcta #}
```

## Filtros que NO Existen en Pebble y Soluciones Alternativas

A diferencia de otros motores de plantillas como Thymeleaf o Jinja2, Pebble tiene un conjunto limitado de filtros integrados. Aquí documentamos filtros comunes que **NO existen** en Pebble y cómo solucionarlo.

### ❌ Filtros que NO Existen

#### 1. `truncate` o `truncatewords`

**NO existe en Pebble:**
```twig
{{ texto | truncate(100) }}  {# ❌ NO FUNCIONA #}
{{ texto | truncatewords(20) }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Usar `slice`** (cortado simple)
```twig
{{ descripcion | slice(0, 100) }}
{# Corta en el carácter 100, puede cortar palabras #}
```

**Opción B: Hacer truncate en el Controller**
```java
@GetMapping("/productos")
public String lista(Model model) {
    List<Product> productos = productoServicio.findAll();
    productos.forEach(p -> {
        if (p.getDescripcion() != null && p.getDescripcion().length() > 100) {
            p.setDescripcion(p.getDescripcion().substring(0, 100) + "...");
        }
    });
    model.addAttribute("productos", productos);
    return "productos/lista";
}
```

**Opción C: Crear filtro personalizado** (ver sección Filtros Personalizados)
```java
private static class TruncateFilter implements Filter {
    @Override
    public Object apply(Object input, Map<String, Object> args, ...) {
        if (input == null) return "";
        String text = input.toString();
        int length = 100;
        if (args.containsKey("length")) {
            length = ((Number) args.get("length")).intValue();
        }
        if (text.length() <= length) return text;
        return text.substring(0, length) + "...";
    }
}
```

#### 2. `striptags` (Eliminar HTML)

**NO existe en Pebble:**
```twig
{{ htmlContent | striptags }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Usar librería en el Controller**
```java
import org.jsoup.Jsoup;

@GetMapping("/articulos")
public String lista(Model model) {
    List<Articulo> articulos = articuloServicio.findAll();
    articulos.forEach(a -> {
        String textoLimpio = Jsoup.parse(a.getContenido()).text();
        a.setContenidoLimpio(textoLimpio);
    });
    model.addAttribute("articulos", articulos);
    return "articulos/lista";
}
```

**Opción B: Crear filtro personalizado con Jsoup**
```java
private static class StripTagsFilter implements Filter {
    @Override
    public Object apply(Object input, Map<String, Object> args, ...) {
        if (input == null) return "";
        return Jsoup.parse(input.toString()).text();
    }
}
```

#### 3. `pluralize` (Pluralización)

**NO existe en Pebble:**
```twig
{{ count }} producto{{ count | pluralize }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Condicional simple**
```twig
{{ count }} producto{% if count != 1 %}s{% endif %}
{{ usuarios | length }} usuario{% if usuarios | length != 1 %}s{% endif %}
```

**Opción B: Operador ternario**
```twig
{{ count }} producto{{ count == 1 ? '' : 's' }}
{{ items | length }} item{{ items | length == 1 ? '' : 's' }}
```

**Opción C: Función de internacionalización**
```twig
{# En messages.properties:
   productos.count.singular=producto
   productos.count.plural=productos
#}
{{ count }} {{ count == 1 ? i18n('productos.count.singular') : i18n('productos.count.plural') }}
```

#### 4. `currency` o `money`

**NO existe en Pebble:**
```twig
{{ precio | currency }}  {# ❌ NO FUNCIONA #}
{{ total | money('EUR') }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Usar filtro personalizado `formatPrice`** (implementado en el proyecto)
```twig
{{ precio | formatPrice }}
{# Salida: 99,99 € #}
```

**Opción B: Usar `numberformat` con sufijo manual**
```twig
{{ precio | numberformat('0.00') }} €
{# Salida: 99.99 € (sin separador de miles) #}
```

**Opción C: Formatear en el Controller**
```java
import java.text.NumberFormat;
import java.util.Locale;

@GetMapping("/productos")
public String lista(Model model) {
    NumberFormat formatter = NumberFormat.getCurrencyInstance(new Locale("es", "ES"));
    List<Product> productos = productoServicio.findAll();
    productos.forEach(p -> p.setPrecioFormateado(formatter.format(p.getPrecio())));
    model.addAttribute("productos", productos);
    return "productos/lista";
}
```

#### 5. `slugify` (Convertir a URL-friendly)

**NO existe en Pebble:**
```twig
{{ titulo | slugify }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Crear slug en el Controller**
```java
import java.text.Normalizer;

public String slugify(String text) {
    String normalized = Normalizer.normalize(text, Normalizer.Form.NFD);
    String slug = normalized.replaceAll("[^\\p{ASCII}]", "")
                            .toLowerCase()
                            .replaceAll("[^a-z0-9]+", "-")
                            .replaceAll("^-|-$", "");
    return slug;
}

@GetMapping("/productos")
public String lista(Model model) {
    List<Product> productos = productoServicio.findAll();
    productos.forEach(p -> p.setSlug(slugify(p.getNombre())));
    model.addAttribute("productos", productos);
    return "productos/lista";
}
```

**Opción B: Generar slug al guardar en la base de datos**
```java
@Entity
public class Product {
    private String nombre;
    private String slug;
    
    @PrePersist
    @PreUpdate
    private void generateSlug() {
        this.slug = slugify(this.nombre);
    }
}
```

#### 6. `date` con zonas horarias

**Limitado en Pebble:**
```twig
{{ fecha | date('dd/MM/yyyy HH:mm z') }}  {# Formato limitado #}
{{ fecha | date('dd/MM/yyyy HH:mm', 'Europe/Madrid') }}  {# ❌ NO soporta timezone #}
```

**✅ Soluciones:**

**Opción A: Filtro personalizado `formatDate`** (implementado en el proyecto)
```twig
{{ compra.fechaCompra | formatDate }}
{# Salida: 15 nov 2025, 14:30 (con locale español) #}
```

**Opción B: Formatear en el Controller con ZonedDateTime**
```java
import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;
import java.time.ZoneId;

@GetMapping("/eventos")
public String lista(Model model) {
    DateTimeFormatter formatter = DateTimeFormatter
        .ofPattern("dd MMM yyyy, HH:mm z")
        .withZone(ZoneId.of("Europe/Madrid"));
    
    List<Evento> eventos = eventoServicio.findAll();
    eventos.forEach(e -> {
        String fechaFormateada = e.getFecha().format(formatter);
        e.setFechaFormateada(fechaFormateada);
    });
    model.addAttribute("eventos", eventos);
    return "eventos/lista";
}
```

#### 7. `wordcount` (Contar palabras)

**NO existe en Pebble:**
```twig
{{ texto | wordcount }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Calcular en el Controller**
```java
@GetMapping("/articulos")
public String lista(Model model) {
    List<Articulo> articulos = articuloServicio.findAll();
    articulos.forEach(a -> {
        int palabras = a.getContenido().split("\\s+").length;
        a.setNumeroPalabras(palabras);
    });
    model.addAttribute("articulos", articulos);
    return "articulos/lista";
}
```

**Opción B: Crear filtro personalizado**
```java
private static class WordCountFilter implements Filter {
    @Override
    public Object apply(Object input, Map<String, Object> args, ...) {
        if (input == null) return 0;
        String text = input.toString().trim();
        if (text.isEmpty()) return 0;
        return text.split("\\s+").length;
    }
}
```

```twig
{# Usar con filtro personalizado #}
{{ articulo.contenido | wordcount }} palabras
```

#### 8. `random` (Elemento aleatorio)

**NO existe en Pebble:**
```twig
{{ productos | random }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Seleccionar aleatorio en el Controller**
```java
import java.util.Random;

@GetMapping("/")
public String index(Model model) {
    List<Product> productos = productoServicio.findAll();
    
    if (!productos.isEmpty()) {
        Random random = new Random();
        Product productoAleatorio = productos.get(random.nextInt(productos.size()));
        model.addAttribute("productoDestacado", productoAleatorio);
    }
    
    return "index";
}
```

**Opción B: Query aleatoria en la base de datos**
```java
public interface ProductRepository extends JpaRepository<Product, Long> {
    @Query(value = "SELECT * FROM products ORDER BY RANDOM() LIMIT 1", nativeQuery = true)
    Product findRandomProduct();
}
```

#### 9. `sha1`, `sha256`, `md5` (Hashing)

**NO existe en Pebble:**
```twig
{{ email | md5 }}  {# ❌ NO FUNCIONA #}
{{ password | sha256 }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**IMPORTANTE: ⚠️ Nunca hashear en la vista. Siempre en el backend.**

```java
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import java.security.MessageDigest;

// Para passwords (BCrypt)
@Autowired
private BCryptPasswordEncoder passwordEncoder;

String hashedPassword = passwordEncoder.encode(plainPassword);

// Para otros casos (MD5, SHA)
public String md5(String input) {
    try {
        MessageDigest md = MessageDigest.getInstance("MD5");
        byte[] hash = md.digest(input.getBytes());
        StringBuilder hexString = new StringBuilder();
        for (byte b : hash) {
            hexString.append(String.format("%02x", b));
        }
        return hexString.toString();
    } catch (Exception e) {
        return null;
    }
}
```

#### 10. `default_if_none` (Similar a `default` pero solo para null)

**Pebble tiene `default` pero funciona diferente:**
```twig
{# default funciona para null Y empty string #}
{{ variable | default('valor') }}

{# ❌ NO existe: default_if_none (solo para null) #}
{{ variable | default_if_none('valor') }}  {# ❌ NO FUNCIONA #}
```

**✅ Soluciones:**

**Opción A: Usar condicional `is not null`**
```twig
{% if variable is not null %}
    {{ variable }}
{% else %}
    valor por defecto
{% endif %}
```

**Opción B: Usar `default` (funciona para null y empty)**
```twig
{{ variable | default('valor') }}
{# Funciona para null, "", y colecciones vacías #}
```

### Resumen de Alternativas

| Filtro Faltante | Solución Recomendada | Dificultad |
|-----------------|---------------------|------------|
| `truncate` | Usar `slice` o filtro personalizado | ⭐ Fácil |
| `striptags` | Jsoup en Controller o filtro personalizado | ⭐⭐ Media |
| `pluralize` | Operador ternario `? :` | ⭐ Fácil |
| `currency` | Filtro personalizado `formatPrice` | ⭐⭐ Media |
| `slugify` | Generar en Controller o @PrePersist | ⭐⭐ Media |
| `date` con timezone | Filtro personalizado o formatear en Controller | ⭐⭐ Media |
| `wordcount` | Calcular en Controller | ⭐ Fácil |
| `random` | Seleccionar en Controller | ⭐ Fácil |
| `sha1/md5` | **Siempre en backend** | ⭐ Fácil |
| `default_if_none` | Usar `is not null` o `default` | ⭐ Fácil |

### Filosofía de Pebble

Pebble sigue el principio de **"Lógica en el Controller, Presentación en la Vista"**:

❌ **NO hacer en la vista:**
- Lógica de negocio compleja
- Operaciones de base de datos
- Transformaciones pesadas de datos
- Cálculos complicados

✅ **SÍ hacer en la vista:**
- Formateo simple de presentación
- Condicionales de visualización
- Iteración sobre datos ya preparados
- Aplicación de estilos CSS condicionales

### Cuándo Crear Filtros Personalizados

**✅ Crear filtro personalizado cuando:**
- El formato es específico de la aplicación (ej: `formatPrice` con símbolo €)
- Se usa frecuentemente en múltiples vistas
- La transformación es pura presentación
- No requiere acceso a servicios o base de datos

**❌ NO crear filtro personalizado cuando:**
- Requiere lógica de negocio
- Necesita acceso a la base de datos
- Se usa solo en una o dos vistas (hacerlo en el Controller)
- Puede comprometer la seguridad

### Mejores Prácticas

#### 1. Preparar Datos en el Controller

```java
// ✅ BUENO: Preparar datos con toda la información necesaria
@GetMapping("/productos")
public String lista(Model model) {
    List<Product> productos = productoServicio.findAll();
    productos.forEach(p -> {
        p.setPrecioFormateado(formatPrice(p.getPrecio()));
        p.setDescripcionCorta(truncate(p.getDescripcion(), 100));
        p.setFechaFormateada(formatDate(p.getFechaCreacion()));
    });
    model.addAttribute("productos", productos);
    return "productos/lista";
}

// ❌ MALO: Dejar todo para la vista
@GetMapping("/productos")
public String lista(Model model) {
    model.addAttribute("productos", productoServicio.findAll());
    return "productos/lista";
}
```

#### 2. Usar DTOs para Datos Complejos

```java
// DTO con datos ya formateados
public class ProductoListadoDTO {
    private Long id;
    private String nombre;
    private String precioFormateado;      // Ya formateado
    private String descripcionCorta;       // Ya truncada
    private String imagenUrl;
    private boolean disponible;
    
    public static ProductoListadoDTO fromEntity(Product p) {
        ProductoListadoDTO dto = new ProductoListadoDTO();
        dto.setId(p.getId());
        dto.setNombre(p.getNombre());
        dto.setPrecioFormateado(formatPrice(p.getPrecio()));
        dto.setDescripcionCorta(truncate(p.getDescripcion(), 100));
        dto.setImagenUrl(p.getImagenOrDefault());
        dto.setDisponible(p.getCompra() == null);
        return dto;
    }
}

// En el Controller
@GetMapping("/productos")
public String lista(Model model) {
    List<ProductoListadoDTO> productos = productoServicio.findAll()
        .stream()
        .map(ProductoListadoDTO::fromEntity)
        .toList();
    model.addAttribute("productos", productos);
    return "productos/lista";
}

// En la vista - datos ya listos
{{ producto.precioFormateado }}
{{ producto.descripcionCorta }}
```

#### 3. Documentar Filtros Personalizados

```java
/**
 * Filtro personalizado para formatear precios en formato español.
 * 
 * Uso: {{ precio | formatPrice }}
 * Entrada: Number (Double, Float, Integer)
 * Salida: String con formato "1.234,56 €"
 * 
 * Ejemplos:
 *   99.99 -> "99,99 €"
 *   1599.50 -> "1.599,50 €"
 *   null -> "0,00 €"
 */
private static class FormatPriceFilter implements Filter { ... }
```

---

**Actualizado con ejemplos reales:** Noviembre 2025  
**Proyecto:** WalaDaw Marketplace


