# Taller de APIs y Postman

Juan Jose Sanchez  
1113860073
Ingeniería de Software II — Cotecnova

## Marco conceptual

### ¿Qué es una API REST?

Una API permite que diferentes aplicaciones se comuniquen entre sí siguiendo una serie de reglas, 
una API REST utiliza el estilo de arquitectura REST para organizar esa comunicación, normalmente 
mediante HTTP, trabaja con recursos que represenstan la informacion con la que vamos a interactuar,
como seria usuarios, publicaciones o productos. 

**Fuente consultada:**https://aws.amazon.com/what-is/restful-api/

## Métodos HTTP

| Método | Operación CRUD | Qué hace |
|---|---|---|
| GET | Read (Leer) | Solicita y consulta información de un recurso sin modificarlo. |
| POST | Create (Crear) | Envía información al servidor para crear un nuevo recurso. |
| PUT | Update (Actualizar) | Reemplaza o actualiza de forma completa un recurso existente. |
| PATCH | Update (Actualizar) | Modifica solamente una parte específica de un recurso. |
| DELETE | Delete (Eliminar) | Elimina un recurso existente. |

Por ejemplo, si una API administra usuarios, `GET /usuarios/1` consulta el usuario número 1, mientras que `DELETE /usuarios/1` solicita eliminarlo.

**Fuente consultada:** https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods



## Códigos de estado

Los códigos de estado HTTP permiten saber qué ocurrió después de realizar una petición a un servidor.

| Familia | Significado | Ejemplo |
|---|---|---|
| 1xx | Respuestas informativas | 100 Continue |
| 2xx | La petición se procesó correctamente | 200 OK |
| 3xx | Redirecciones | 301 Moved Permanently |
| 4xx | Error relacionado con la petición del cliente | 404 Not Found |
| 5xx | Error producido en el servidor | 500 Internal Server Error |


La diferencia principal entre los errores 4xx y 5xx está en el origen del problema. 
Un código 4xx normalmente indica que el servidor recibió una petición que no puede atender
por alguna condición relacionada con lo enviado por el cliente, por ejemplo solicitar 
un recurso que no existe. En cambio, un código 5xx indica que el servidor tuvo un problema interno al 
intentar procesar una petición que podría ser válida.

Por eso un código diferente de 200 no significa automáticamente que una prueba haya fallado.
Si se solicita intencionalmente un recurso inexistente y se espera un 404, recibir un 404 sería el 
comportamiento correcto de la API.

**Fuente consultada:** https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

## Cómo reproducir este taller

1. Instalar Postman.
2. Descargar o clonar este repositorio.
3. Abrir Postman.
4. Importar el archivo `coleccion.json`.
5. Abrir la colección `Taller-API`.
6. Ejecutar las peticiones incluidas en la colección.
7. Revisar los códigos de estado, cuerpos de respuesta y resultados de las pruebas automáticas.

## Archivos de este repositorio

- `README.md`: contiene el marco conceptual, métodos HTTP y códigos de estado.
- `hallazgos.md`: contiene los resultados obtenidos durante las pruebas realizadas en Postman.
- `conclusiones.md`: contiene las conclusiones de las tareas de investigación y experimentación.
- `coleccion.json`: colección de Postman exportada en formato Collection v2.1.
- `evidencias/`: contiene las capturas de pantalla solicitadas durante el taller.