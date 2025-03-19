# Introducción

## Descripción General

Esta API proporciona acceso programático a nuestro sistema, permitiendo a los desarrolladores integrar nuestras funcionalidades en sus aplicaciones de manera sencilla y eficiente.

## Base URL

Todas las peticiones deben realizarse a la siguiente URL base:

```
https://api.ejemplo.com/v1
```

## Autenticación

Nuestra API utiliza OAuth 2.0 para autenticación. Para obtener acceso, debes:

1. Registrar tu aplicación en nuestro [portal de desarrolladores](https://developers.ejemplo.com)
2. Obtener tus credenciales (client_id y client_secret)
3. Solicitar un token de acceso

### Ejemplo de solicitud de token

```bash
curl -X POST https://api.ejemplo.com/v1/oauth/token \
  -d "grant_type=client_credentials" \
  -d "client_id=TU_CLIENT_ID" \
  -d "client_secret=TU_CLIENT_SECRET"
```

### Ejemplo de respuesta

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

## Formato de Respuesta

Todas las respuestas se devuelven en formato JSON con los siguientes campos estándar:

| Campo | Descripción |
|-------|-------------|
| `status` | Estado de la respuesta ("success" o "error") |
| `data` | Los datos solicitados (si la petición fue exitosa) |
| `error` | Información sobre el error (si la petición falló) |

## Versionado

Nuestra API está versionada para garantizar la compatibilidad. La versión actual es `v1`.