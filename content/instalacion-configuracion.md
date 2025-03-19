# Instalación y Configuración 
 
## Instalación 
 
```bash 
# Clonar el repositorio 
git clone https://github.com/tuorganizacion/tuapi.git 
 
# Navegar al directorio 
cd tuapi 
 
# Compilar el proyecto 
./mvnw clean install 
``` 
 
## Configuración 
 
### Archivo application.properties 
 
```properties 
# Configuración de la base de datos 
spring.datasource.url=jdbc:postgresql://localhost:5432/mibasededatos 
spring.datasource.username=usuario 
spring.datasource.password=contraseña 
 
# Configuración JPA 
spring.jpa.hibernate.ddl-auto=update 
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect 
``` 
