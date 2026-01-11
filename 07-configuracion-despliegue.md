- [7. Configuracion y Despliegue](#7-configuracion-y-despliegue)
  - [7.1 Configuracion Multi-Entorno](#71-configuracion-multi-entorno)
  - [7.2 Variables de Entorno](#72-variables-de-entorno)
  - [7.3 Docker y Contenedores](#73-docker-y-contenedores)
  - [7.4 Despliegue JAR](#74-despliegue-jar)


# 7. Configuracion y Despliegue

## 7.1 Configuracion Multi-Entorno

Las aplicaciones web pasan por diferentes entornos durante su ciclo de vida.

**application.properties (base):**

```properties
app.name=Mi Aplicacion
server.port=8080
pebble.suffix=.peb
```

**application-dev.properties:**

```properties
spring.profiles.active=dev
spring.datasource.url=jdbc:h2:mem:devdb
spring.jpa.hibernate.ddl-auto=create-drop
pebble.cache=false
```

**application-prod.properties:**

```properties
spring.profiles.active=prod
spring.datasource.url=jdbc:postgresql://db:5432/miapp
spring.datasource.username=${DB_USER}
spring.datasource.password=${DB_PASS}
spring.jpa.hibernate.ddl-auto=validate
pebble.cache=true
```

## 7.2 Variables de Entorno

Permiten configurar la aplicacion sin modificar codigo.

```properties
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USER}
```

## 7.3 Docker y Contenedores

Docker permite empaquetar la aplicacion con todas sus dependencias.

**Dockerfile:**

```dockerfile
FROM eclipse-temurin:17-jre-alpine
COPY build/libs/*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

**docker-compose.yml:**

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_DB=miapp
      POSTGRES_USER=user
      POSTGRES_PASSWORD=pass
```

## 7.4 Despliegue JAR

Spring Boot genera un archivo JAR ejecutable.

```bash
./gradlew bootJar
java -jar build/libs/miapp-1.0.0.jar
```

Para produccion:

```bash
java -Dspring.profiles.active=prod -DDB_USER=admin -DDB_PASS=pass build/libs/miapp-1.0.0.jar
```

---

**Recuerda:** Nunca subas credenciales a Git. Usa variables de entorno.
