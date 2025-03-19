# Documentación API Spring Boot

Este proyecto contiene la documentación interactiva para una API REST desarrollada con Spring Boot, utilizando MkDocs con el tema Material para generar un sitio web estático fácil de navegar.

## Características

- **Documentación completa**: Endpoints, modelos de datos, autenticación, ejemplos de uso, etc.
- **Navegación intuitiva**: Interfaz con pestañas y secciones bien organizadas
- **Tema personalizado**: Esquema de colores gris oscuro para lectura confortable
- **Responsive**: Se adapta a dispositivos móviles y de escritorio
- **Búsqueda integrada**: Búsqueda rápida de contenido en toda la documentación

## Requisitos previos

- [Docker](https://www.docker.com/get-started) y Docker Compose
- O alternativamente, Python 3.x con pip para instalación local

## Estructura del proyecto

```
proyecto-docs/
├── content/               # Archivos markdown de la documentación
│   ├── assets/            # Imágenes y recursos
│   ├── css/               # Estilos personalizados
│   ├── index.md           # Página principal
│   └── ...                # Otros archivos de documentación
├── docker-compose.yml     # Configuración de Docker
└── mkdocs.yml             # Configuración de MkDocs
```

## Cómo levantar la documentación con Docker

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/tu-usuario/tu-proyecto-docs.git
   cd tu-proyecto-docs
   ```

2. **Iniciar con Docker Compose**
   ```bash
   docker-compose up
   ```

3. **Acceder a la documentación**
   
   Abre tu navegador y ve a http://localhost:9005

   La documentación se actualizará automáticamente cuando hagas cambios en los archivos markdown.

4. **Detener el servicio**
   ```bash
   # Presiona Ctrl+C en la terminal o ejecuta:
   docker-compose down
   ```

## Instalación local (alternativa a Docker)

Si prefieres no usar Docker:

1. **Instalar MkDocs y el tema Material**
   ```bash
   pip install mkdocs mkdocs-material
   ```

2. **Iniciar el servidor de desarrollo**
   ```bash
   mkdocs serve
   ```

3. **Acceder a la documentación**
   
   Abre tu navegador y ve a http://localhost:8000

## Personalización

- **Cambiar colores**: Modifica `content/css/extra.css`
- **Cambiar contenido**: Edita los archivos markdown en la carpeta `content/`
- **Cambiar configuración**: Ajusta las opciones en `mkdocs.yml`
- **Cambiar logo**: Reemplaza las imágenes en `content/assets/`

## Generar documentación estática

Para generar un sitio web estático que puedas desplegar en cualquier servidor:

```bash
# Con Docker
docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material build

# O localmente
mkdocs build
```

Los archivos generados estarán en la carpeta `site/`.

## Contribuir

1. Haz un fork del repositorio
2. Crea una rama para tu funcionalidad (`git checkout -b nueva-funcionalidad`)
3. Haz commit de tus cambios (`git commit -am 'Añade nueva funcionalidad'`)
4. Haz push a la rama (`git push origin nueva-funcionalidad`)
5. Crea un nuevo Pull Request

## Licencia

[MIT](LICENSE)