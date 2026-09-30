# Taller de APIs y Pruebas con Postman

**Estudiante:** Lisandro Villegas Henao
**Código:** 1113860384
**Asignatura:** Ingeniería de Software II — Cotecnova

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

## Códigos de estado HTTP

Los códigos de estado son respuestas numéricas de tres dígitos que el servidor devuelve para indicar el resultado de una petición. Se clasifican en cinco familias según su primer dígito:

- **1xx (Informativos):** Indican que el servidor recibió la solicitud y la está procesando. *Ejemplo: `100 Continue` (el servidor le dice al cliente que puede continuar enviando el resto de la petición).
- **2xx (Éxito):** Confirman que la petición fue recibida, entendida y procesada correctamente. *Ejemplo: `200 OK` (consulta exitosa) o `201 Created` (recurso creado con éxito).
- **3xx (Redirección):** Indican que el recurso cambió de lugar y el cliente debe ir a otra dirección URL para obtenerlo. *Ejemplo: `301 Moved Permanently` (el recurso se movió de forma definitiva a otra ubicación).
- **4xx (Errores del cliente):** Advierten que el cliente envió información incorrecta, incompleta o pidió un recurso que no existe. *Ejemplo: `404 Not Found` (la dirección solicitada no existe en el servidor).
- **5xx (Errores del servidor):** Señalan que la petición llegó bien, pero el servidor sufrió un problema interno en su código o base de datos y no pudo responder. *Ejemplo: `500 Internal Server Error` (fallo inesperado en el backend).

### Asignación de culpa entre errores 4xx y 5xx

Entender la diferencia entre estas dos familias es clave porque define de quién es la responsabilidad del fallo y qué se debe hacer en la práctica:

- **En un error 4xx (Culpa del Cliente):** El problema está en lo que el cliente envió (por ejemplo, escribir mal la URL o enviar un dato que falta). En la práctica, **volver a intentar la misma petición exactamente igual NO sirve de nada**, porque el servidor la seguirá rechazando. El cliente debe modificar los datos antes de reenviar.
- **En un error 5xx (Culpa del Servidor):** La petición del cliente está bien construida y cumple con las reglas, pero el servidor colapsó internamente. En la práctica, **aquí puede tener sentido reintentar más tarde**, ya que si el equipo de backend corrige el fallo o el servidor recupera la disponibilidad, la misma petición podría funcionar sin cambiarle nada.

Es como pedir comida a domicilio: un error 4xx es pedir algo que no está en el menú (el cliente se equivocó y debe cambiar la orden), mientras que un error 5xx es que se vaya la luz en la cocina del restaurante (la orden estaba bien, pero el restaurante tuvo un problema interno).

Fuentes consultadas:

- IBM Docs, *Códigos de estado y expresiones de razón*: https://ibm.com/docs/es/SSGMCP_6.1.0/fundamentals/web/dfhtl_httpstatus.html
- Infomaniak, *Comprender los errores HTTP*: https://infomaniak.com/es/asistencia/faq/257/comprender-los-errores-http

## Cómo reproducir este taller

Para ejecutar esta colección y verificar todas las pruebas de la API en Postman, sigue estos pasos:

1. **Clonar el repositorio:** Abre una terminal y ejecuta el siguiente comando para clonar el proyecto en tu máquina local:
   ```bash
   git clone https://github.com/tu-usuario/taller-postman-villegas.git

Abrir Postman.

Importar la colección:

Haz clic en el botón Import (esquina superior izquierda).

Selecciona el archivo coleccion.json ubicado en la raíz de este proyecto.

Ejecutar las pruebas:

Haz clic derecho sobre la colección Taller-API importada y selecciona Run collection (Collection Runner).

Presiona Run Taller-API para verificar la ejecución automática de las peticiones y los resultados de los scripts en la pestaña Test Results.

## Archivos de este repositorio

README.md: Documento principal con la presentación, marco conceptual, tabla de métodos HTTP, clasificación de códigos de estado y guía de ejecución.

hallazgos.md: Registro de experimentos prácticos, análisis de pruebas de frontera (404), comparación PUT vs. PATCH, persistencia tras DELETE, rutas anidadas y los 3 scripts de pruebas automatizadas (pm.expect).

conclusiones.md: Análisis sobre la importancia de la idempotencia en servicios REST, inspección de cabeceras de respuesta HTTP (Headers) y fuentes bibliográficas consultadas.

coleccion.json: Archivo exportado de Postman v2.1 que contiene la estructura completa de carpetas, peticiones y scripts de validación.

evidencias/: Carpeta que almacena las capturas de pantalla tomadas durante la ejecución de las pruebas en Postman. 