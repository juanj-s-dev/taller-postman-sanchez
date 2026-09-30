# Hallazgos del taller

## Tabla de peticiones

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
| --- | --- | --- | --- | --- |
| 1 | GET /posts/1 | 200 | 200 | Sí |
| 2 | GET /posts | 200 | 200 | Sí |
| 3 | GET /posts/9999 | 404 | 404 | Sí |
| 4 | POST /posts | 201 | 201 | Sí |
| 5 | PUT /posts/1 | 200 | 200 | Sí |
| 6 | PATCH /posts/1 | 200 | 200 | Sí |
| 7 | DELETE /posts/1 | 200 | 200 | Sí |

## Observación del POST

La petición POST se ejecutó cinco veces y en todas las ejecuciones la API devolvió el código `201 Created` y el id `101`.

Esto indica que JSONPlaceholder simula la creación del recurso, pero no genera ni almacena un nuevo registro persistente en cada ejecución.

En una API real comprobaría que el recurso fue creado realizando posteriormente una petición GET al recurso generado, utilizando el id devuelto por el servidor. También verificaría que los datos enviados coincidan con los datos almacenados.

## Comparación entre PUT y PATCH

### Respuesta PUT

Se envió únicamente el campo `title`:

```json
{
  "title": "Titulo actualizado con PUT"
}
```

La respuesta obtenida fue:

```json
{
  "title": "Titulo actualizado con PUT",
  "id": 1
}
```

Al utilizar PUT enviando únicamente el campo `title`, la respuesta ya no incluyó campos originales como `userId` y `body`.

### Respuesta PATCH

Se envió únicamente el campo `title`:

```json
{
  "title": "Titulo actualizado con PATCH"
}
```

La respuesta obtenida fue:

```json
{
  "userId": 1,
  "id": 1,
  "title": "Titulo actualizado con PATCH",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

En este caso, PATCH modificó solamente el campo `title` y conservó los demás campos originales del recurso.

Por esta razón utilizaría PATCH para corregir un error de escritura en un solo campo, ya que permite realizar una modificación parcial sin reemplazar el resto de la información.

## Tarea 10 - Valores límite

Al probar los recursos de la API encontré que:

- `GET /posts/100` devuelve `200 OK`.
- `GET /posts/101` devuelve `404 Not Found`.

Por lo tanto, el id 100 es el valor válido más alto y el id 101 es el primer valor fuera del rango existente.

Este tipo de prueba se conoce como prueba de valores límite o *Boundary Value Analysis*. Se utiliza para comprobar el comportamiento del sistema justo en los puntos donde una condición cambia de válida a inválida.

Los defectos suelen concentrarse cerca de estos límites porque es común que existan errores al definir condiciones como menor que, menor o igual que, mayor que o mayor o igual que.

## Tarea 11 - Exploración de otros recursos

Además del recurso `/posts`, exploré otros recursos disponibles en JSONPlaceholder.

### Usuarios

La petición:

`GET /users`

devolvió `200 OK`.

La respuesta contiene una colección de usuarios con información como `id`, `name`, `username`, `email`, dirección, teléfono, sitio web y empresa.

### Tareas

La petición:

`GET /todos`

devolvió `200 OK`.

Cada elemento contiene campos como `userId`, `id`, `title` y `completed`. El campo `completed` indica mediante `true` o `false` si la tarea está completada.

### Ruta anidada

También probé:

`GET /posts/1/comments`

La petición devolvió `200 OK` y una colección de comentarios relacionados con la publicación número 1.

Cada comentario incluye campos como `postId`, `id`, `name`, `email` y `body`.

La estructura de la URL permite entender la relación entre los recursos. En `/posts/1/comments`, primero se identifica la publicación con id 1 y después se solicitan los comentarios asociados a esa publicación.


## Tarea 13 - Pruebas automáticas

Se agregaron cuatro pruebas automáticas a la petición `GET /posts/1`.

```javascript
pm.test("El estado es 200", function () {
    pm.response.to.have.status(200);
});

const jsonData = pm.response.json();

pm.test("La respuesta contiene el campo id", function () {
    pm.expect(jsonData).to.have.property("id");
});

pm.test("El campo title es de tipo texto", function () {
    pm.expect(jsonData.title).to.be.a("string");
});

pm.test("El tiempo de respuesta es menor a 2000 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(2000);
});
```

Las pruebas verifican lo siguiente:

1. Que la respuesta HTTP tenga código `200`.
2. Que el JSON contenga el campo `id`.
3. Que el campo `title` sea de tipo texto (`string`).
4. Que el tiempo de respuesta sea menor a 2000 milisegundos.

Al ejecutar la petición, Postman mostró `4/4`, indicando que las cuatro pruebas se ejecutaron correctamente.