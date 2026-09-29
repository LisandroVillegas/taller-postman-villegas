# Taller de APIs y Pruebas con Postman

**Estudiante:** Lisandro Villegas Henao


**Asignatura:** Ingeniería de Software II  

## Marco conceptual

Una API es como un mesero en un restaurante: recibe lo que pides, se lo lleva a la cocina (el servidor) y te regresa la respuesta sin que tengas que saber cómo funciona todo por dentro. La sigla REST significa Transferencia de Estado Representacional, y no es un protocolo rígido ni un estándar, sino una guía de buenas prácticas para construir APIs web. Para que sea RESTful debe cumplir principios como la arquitectura cliente-servidor, que establece que el cliente y el servidor son componentes totalmente separados que pueden evolucionar de forma independiente, y la comunicación sin estado (*stateless*), lo que significa que cada petición es autónoma y el servidor no guarda memoria de solicitudes anteriores. REST utiliza preferiblemente el protocolo HTTP y el formato JSON para intercambiar datos de forma liviana. En este modelo, el **recurso** es el elemento o dato que quieres consultar o modificar (como una publicación), mientras que el **endpoint** es la URL o dirección específica donde lo solicitas (como `/posts/1`). Un ejemplo real ocurre cuando abro la app de Spotify en mi celular: la aplicación se conecta a la API para pedir los datos de una lista de reproducción o buscar un artista, y el servidor le devuelve esa información en formato JSON para mostrarla en la pantalla.

Fuente consultada:
- Red Hat, ¿Qué es una API REST?: https://www.redhat.com/es/topics/api/what-is-a-rest-api
- IBM, ¿Qué es un endpoint de API?: https://www.ibm.com/mx-es/think/topics/api-endpoint

## Métodos HTTP

| Método | Operación CRUD | Qué hace |
|---|---|---|
| GET | Read | Consulta y trae la información de un registro o lista desde el servidor sin modificar ningún dato. |
| POST | Create | Envía un paquete de datos para guardar y registrar una entidad completamente nueva en el servidor. |
| PUT | Update | Sobrescribe un registro existente por completo. Se le debe enviar el objeto completo; si un campo no se envía, ese dato se borra o se reemplaza por valor nulo. |
| PATCH | Update | Modifica únicamente los datos específicos que se envían. Los campos que no se incluyan en la petición se mantienen intactos sin sufrir ningún cambio. |
| DELETE | Delete | Solicita eliminar o remover un registro específico alojado en el servidor. |

Fuente contultada:
- MDN Web Docs, Métodos de petición HTTP: https://developer.mozilla.org/es/docs/Web/HTTP/Methods