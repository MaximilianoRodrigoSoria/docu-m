# Instalación y Configuración

## Requisitos Previos

- Java 21
- Maven 3.8+
- Base de datos PostgreSQL (opcional)
- Lombok

## Instalación

### Clonar el Repositorio

```bash
git clone https://github.com/tu-organizacion/example-api.git
cd example-api
```

### Compilar el Proyecto

```bash
mvn clean install
```

## Configuración

### application.properties

El archivo de configuración principal se encuentra en `src/main/resources/application.properties`:

```properties
# Configuración del servidor
server.port=8080
server.servlet.context-path=/example-api

# Versión de la API
api.version=v1
api.base-path=/api/${api.version}

# Configuración de la base de datos
spring.datasource.url=jdbc:postgresql://localhost:5432/exampledb
spring.datasource.username=postgres
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# Configuración para Java 21
spring.threads.virtual.enabled=true

# Configuración de logging
logging.level.org.springframework=INFO
logging.level.com.example=DEBUG
```

### Perfiles de Entorno

La aplicación soporta diferentes perfiles de entorno:

| Perfil | Descripción |
|--------|-------------|
| `dev` | Entorno de desarrollo local |
| `test` | Entorno de pruebas |
| `prod` | Entorno de producción |

Para ejecutar la aplicación con un perfil específico:

```bash
java -jar target/example-api.jar --spring.profiles.active=dev
```

## Ejecución

### Ejecutar en Modo Desarrollo

```bash
mvn spring-boot:run
```

Por defecto, la API estará disponible en:

```
http://localhost:8080/example-api/api/v1
```

### Contenedor Docker (opcional)

También puedes ejecutar la aplicación como un contenedor Docker:

```bash
# Construir la imagen
docker build -t example-api .

# Ejecutar el contenedor
docker run -p 8080:8080 example-api
```

## Verificación de la Instalación

Para verificar que la API está funcionando correctamente, puedes hacer una petición al endpoint de estado:

```bash
curl http://localhost:8080/example-api/api/v1/health
```

Respuesta esperada:

```json
{
  "status": "UP",
  "version": "1.0.0",
  "timestamp": "2025-03-19T12:00:00Z"
}
```