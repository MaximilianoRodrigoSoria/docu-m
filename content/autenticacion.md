# Autenticación 
 
La API utiliza [tipo de autenticación] para proteger los endpoints. 
 
## Obtención de credenciales 
 
[Instrucciones para obtener credenciales] 
 
## Flujo de autenticación 
 
```plaintext 
POST /api/auth/login 
Content-Type: application/json 
 
{ 
  "username": "ejemplo", 
  "password": "contraseña" 
} 
``` 
 
## Ejemplo de uso del token 
 
```plaintext 
GET /api/recurso 
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9... 
``` 
