# Conclusiones del taller

## Tarea 8 - Idempotencia

Un método HTTP es idempotente cuando ejecutar varias veces la misma 
petición produce el mismo estado final que ejecutarla una sola vez.

Los métodos GET, PUT y DELETE son idempotentes. 
POST no es idempotente y PATCH no garantiza serlo, ya que su
resultado depende del tipo de modificación que realice.

### Comprobación en Postman

Al repetir varias veces la misma petición PUT, 
la respuesta se mantuvo igual y no se observó ningún cambio adicional. 
Esto coincide con el comportamiento de un método idempotente, porque repetir la 
operación no cambia el estado final.

Al repetir varias veces la misma petición POST, JSONPlaceholder 
volvió a responder con 201 Created y el id 101. No se crearon identificadores 
nuevos visibles, debido a que JSONPlaceholder simula las operaciones y no guarda 
permanentemente los recursos.



## Tarea 9 - Cabeceras de la respuesta

Al revisar los Headers de la respuesta de la petición `GET /posts/1`, 
encontré varias cabeceras. Seleccioné las siguientes:

### Content-Type

La cabecera `Content-Type` indica el tipo de contenido que está enviando 
el servidor. En esta respuesta su valor fue:

`application/json; charset=utf-8`

Esto significa que la respuesta está en formato JSON y utiliza codificación UTF-8.

Esta cabecera es importante al probar una API porque permite comprobar 
que el servidor está devolviendo la información en el formato esperado. 

## Tarea 12 - Importancia de observar una prueba fallar

Es importante comprobar que una prueba pueda fallar antes de confiar en ella, porque así se verifica que realmente está evaluando la condición definida. En este caso, cuando la prueba esperaba un código 201 pero la API respondió 200, Postman mostró el resultado como fallido. Esto demostró que la prueba podía detectar un resultado diferente al esperado.
Por ejemplo, si una API debería devolver JSON pero responde con HTML, podría 
existir un error en el endpoint o en el servidor.

### Cache-Control

La cabecera `Cache-Control` indica cómo puede almacenarse temporalmente una respuesta en caché.

En esta petición apareció:

`max-age=43200`

Esto indica que la respuesta puede considerarse válida en caché durante un periodo 
determinado antes de tener que solicitarla nuevamente al servidor.

### ETag

La cabecera `ETag` funciona como un identificador de una versión específica de un recurso.

El servidor puede utilizar este valor para comprobar si un recurso ha cambiado desde 
la última vez que fue solicitado. Esto ayuda a evitar descargar nuevamente información 
que no ha cambiado.

## Reflexiones finales

### ¿Qué le faltaría a la tabla de la Fase 2 para ser un plan de pruebas formal?

La tabla utilizada durante el taller ya contiene elementos básicos de un caso de prueba, como la petición realizada, el resultado esperado y el resultado obtenido.

Para convertirse en un plan de pruebas más formal debería incluir información adicional como el identificador del caso de prueba, objetivo de la prueba, precondiciones, datos de entrada, pasos de ejecución, resultado esperado, resultado real, estado de la prueba, prioridad y observaciones.

También sería útil identificar quién ejecutó la prueba, la fecha de ejecución y el entorno utilizado.

### ¿Por qué un 404 puede ser una buena noticia y un 200 puede ser un defecto?

Un código 404 puede representar un resultado correcto cuando el objetivo de la prueba es comprobar qué sucede al solicitar un recurso que no existe.

Por ejemplo, en `GET /posts/9999` se esperaba recibir un código 404 y la API respondió con 404, por lo que el caso de prueba pasó correctamente.

En cambio, un código 200 puede representar un defecto si el comportamiento esperado era diferente. Si se solicita un recurso inexistente y el servidor responde 200 indicando que todo fue correcto, aunque el recurso no exista, el resultado no coincide con lo esperado.

Por esta razón, una prueba no se considera exitosa únicamente por recibir un código 200, sino porque el resultado obtenido coincide con el resultado esperado.