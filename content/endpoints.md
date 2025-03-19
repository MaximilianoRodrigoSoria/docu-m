# Endpoints Detallados

## URL Base

```
http://localhost:8080/example-api/api/v1
```

## Endpoints de la Entidad Example

### GET /examples

Obtiene una lista paginada de todos los ejemplos.

#### Parámetros de Consulta

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|-----------|-------------|
| page | Integer | No | Número de página (por defecto: 0) |
| size | Integer | No | Elementos por página (por defecto: 20) |
| sort | String | No | Campo y dirección de ordenamiento (ej. `descripcion,asc`) |

#### Respuesta

```json
{
  "content": [
    {
      "id": 1,
      "descripcion": "Ejemplo 1"
    },
    {
      "id": 2,
      "descripcion": "Ejemplo 2"
    }
  ],
  "pageable": {
    "pageNumber": 0,
    "pageSize": 20,
    "totalElements": 2,
    "totalPages": 1
  }
}
```

#### Códigos de Estado

| Código | Descripción |
|--------|-------------|
| 200 | OK - Operación exitosa |
| 500 | Internal Server Error - Error en el servidor |

### GET /examples/{id}

Obtiene un ejemplo específico por su ID.

#### Parámetros de Ruta

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|-----------|-------------|
| id | Integer | Sí | ID del ejemplo a consultar |

#### Respuesta

```json
{
  "id": 1,
  "descripcion": "Ejemplo 1"
}
```

#### Códigos de Estado

| Código | Descripción |
|--------|-------------|
| 200 | OK - Operación exitosa |
| 404 | Not Found - Ejemplo no encontrado |
| 500 | Internal Server Error - Error en el servidor |

### POST /examples

Crea un nuevo ejemplo.

#### Cuerpo de la Petición

```json
{
  "descripcion": "Nuevo ejemplo"
}
```

#### Respuesta

```json
{
  "id": 3,
  "descripcion": "Nuevo ejemplo"
}
```

#### Códigos de Estado

| Código | Descripción |
|--------|-------------|
| 201 | Created - Ejemplo creado exitosamente |
| 400 | Bad Request - Error de validación |
| 500 | Internal Server Error - Error en el servidor |

### PUT /examples/{id}

Actualiza un ejemplo existente.

#### Parámetros de Ruta

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|-----------|-------------|
| id | Integer | Sí | ID del ejemplo a actualizar |

#### Cuerpo de la Petición

```json
{
  "descripcion": "Descripción actualizada"
}
```

#### Respuesta

```json
{
  "id": 1,
  "descripcion": "Descripción actualizada"
}
```

#### Códigos de Estado

| Código | Descripción |
|--------|-------------|
| 200 | OK - Ejemplo actualizado exitosamente |
| 400 | Bad Request - Error de validación |
| 404 | Not Found - Ejemplo no encontrado |
| 500 | Internal Server Error - Error en el servidor |

### DELETE /examples/{id}

Elimina un ejemplo existente.

#### Parámetros de Ruta

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|-----------|-------------|
| id | Integer | Sí | ID del ejemplo a eliminar |

#### Códigos de Estado

| Código | Descripción |
|--------|-------------|
| 204 | No Content - Ejemplo eliminado exitosamente |
| 404 | Not Found - Ejemplo no encontrado |
| 500 | Internal Server Error - Error en el servidor |

## Implementación del Controlador

```java
@RestController
@RequestMapping("/api/v1/examples")
@RequiredArgsConstructor
public class ExampleController {

    private final ExampleService exampleService;
    
    @GetMapping
    public ResponseEntity<Page<ExampleDTO>> getAllExamples(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "20") int size,
            @RequestParam(defaultValue = "id,asc") String sort) {
        
        String[] sortParams = sort.split(",");
        Sort.Direction direction = sortParams.length > 1 && sortParams[1].equalsIgnoreCase("desc") 
                ? Sort.Direction.DESC : Sort.Direction.ASC;
        
        Pageable pageable = PageRequest.of(page, size, direction, sortParams[0]);
        Page<ExampleDTO> examples = exampleService.findAll(pageable);
        
        return ResponseEntity.ok(examples);
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<ExampleDTO> getExampleById(@PathVariable Integer id) {
        ExampleDTO example = exampleService.findById(id);
        return ResponseEntity.ok(example);
    }
    
    @PostMapping
    public ResponseEntity<ExampleDTO> createExample(@Valid @RequestBody CreateExampleDTO createExampleDTO) {
        ExampleDTO createdExample = exampleService.create(createExampleDTO);
        return ResponseEntity.status(HttpStatus.CREATED).body(createdExample);
    }
    
    @PutMapping("/{id}")
    public ResponseEntity<ExampleDTO> updateExample(
            @PathVariable Integer id,
            @Valid @RequestBody UpdateExampleDTO updateExampleDTO) {
        
        ExampleDTO updatedExample = exampleService.update(id, updateExampleDTO);
        return ResponseEntity.ok(updatedExample);
    }
    
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteExample(@PathVariable Integer id) {
        exampleService.delete(id);
        return ResponseEntity.noContent().build();
    }
}
```

## Diagrama de Flujo de Peticiones

```mermaid
sequenceDiagram
    participante Cliente
    participante Controller
    participante Service
    participante Repository
    participante Database
    
    Cliente->>Controller: GET /examples/{id}
    Controller->>Service: findById(id)
    Service->>Repository: findById(id)
    Repository->>Database: SELECT * FROM examples WHERE id = ?
    Database-->>Repository: Resultado
    Repository-->>Service: Example entity
    Service-->>Controller: ExampleDTO
    Controller-->>Cliente: JSON Response
```