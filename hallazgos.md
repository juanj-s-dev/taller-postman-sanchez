# Hallazgos del taller

## Tabla de peticiones

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
|---|---|---|---|---|
| 1 | GET /posts/1 | 200 | 200 | Sí |
| 2 | GET /posts | 200 | 200 | Sí |
| 3 | GET /posts/9999 | 404 | 404 | Sí |
| 4 | POST /posts | 201 | 201 | Sí |
| 5 | PUT /posts/1 | 200 | 200 | Sí |
| 6 | PATCH /posts/1 | 200 | 200 | Sí |
| 7 | DELETE /posts/1 | 200 | 200 | Sí |

### Respuesta PUT

```json
{
  "title": "Titulo actualizado con PUT",
  "id": 1
}

### Respuesta PATCH

```json
{
  "userId": 1,
  "id": 1,
  "title": "Titulo actualizado con PATCH",
  "body": "quia et suscipit..."
}

### Observación del POST

La petición POST se ejecutó cinco veces y en todas las ejecuciones la API 
devolvió el código 201 Created y el id 101. Esto indica que JSONPlaceholder simula 
la creación del recurso, pero no genera ni almacena un nuevo registro persistente en cada ejecución.

En una API real comprobaría que el recurso fue creado realizando posteriormente una petición GET al recurso generado, utilizando el id devuelto por el servidor. También verificaría que los datos enviados coincidan con los datos almacenados.