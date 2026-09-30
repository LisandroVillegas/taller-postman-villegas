## Tarea 8: Idempotencia

**Qué es:** Un método es idempotente si repetir la misma petición varias veces deja al servidor en el mismo estado que hacerla una sola vez. La primera vez sí puede cambiar algo las repeticiones ya no  cambian nada más, por ejemplo pulsar el botón del ascensor cinco veces equivale a pulsarlo una  y en cambio dar "Pagar" cinco veces puede generar 5 cobros. 


**Cuáles lo son:** GET es idempotente porque solo lee, no cambia nada. PUT también es idempotente porque reemplaza el recurso porque lo envías, repetirlo deja el mismo resultado. DELETE también es idempotente porque despues de borrar, el recurso ya no existe y borrar de nuevo no cambia el estado (aunque la segunda vez puede dar 404), POST no lo es ya que cada envio puede crear un recurso nuevo y PATCH depende de la modificación aunque MDN lo marca como "NO", ahi en la documentación o bueno en el link de la fuente se puede ver en las tablas.

Fuente: https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Methods/PUT

**Lo que observé en Postman:**
- PUT enviado tres veces: La primera vez pues el PUT si dejó el recurso con el titulo nuevo pero al darle 3 veces más pude notar que no cambió el resultado, el estado quedó igual que después del primer envio, entonces eso es ser idempotente.

- POST enviado cinco veces: siempre devolvió 201 con id 101 ya que JSONPlaceholder solo simula la creación y no guarda nada, por eso el id nunca avanza a 102 o 103 y asi sucesivamente. Lo que pasaria en una API real es que cada POST crearia un recurso nuevo con un id distinto, por eso el POST no es idempotente, ya que repetirlo cambia el estado del servidor.

## Tarea 9: Las cabeceras de la respuesta (Headers)

Al revisar la pestaña Headers de la respuesta en Postman para la petición GET https://jsonplaceholder.typicode.com/posts/1, elegi estas tres cabeceras para investigar:

1. **Content-Type (valor: application/json; charset=utf-8`)**
   Me indica de qué tipo son los datos del cuerpo de la respuesta. El valor application/json me confirma que la API me responde en formato JSON, y charset=utf-8 es la codificación para que las tildes y la ñ se lean correctamente.

2. **Date (valor: Tue, 29 Sep 2026 22:22:11 GMT)**
   Muestra la fecha y hora exacta en que el servidor generó la respuesta en formato GMT. Al revisar la hora en mi reloj (las 5:22 PM o 17:22 en Colombia), noté que sumándole las 5 horas de diferencia horaria corresponde exactamente a las 22:22 GMT. Me sirve para saber el momento exacto en que respondió el servidor.

3. **Access-Control-Allow-Credentials` (valor: true)**
   Es una cabecera de CORS. Le indica al navegador que el código JavaScript de una página puede leer la respuesta aunque lleve credenciales (como cookies o tokens). En mi prueba, Postman la muestra en la respuesta, pero no me bloquea la petición porque Postman no aplica las reglas de un navegador.

### Por qué Content-Type es importante al probar una API

- **Al recibir una respuesta:** Me indica cómo interpretar el cuerpo. Como llegó application/json, Postman pudo dar formato ordenado al JSON. Si llegara otro tipo de dato (como un HTML de error), me daría cuenta de que algo falló.
- **Al enviar una petición:** En POST, PUT y PATCH, le dice al servidor en qué formato va lo que envío. En el POST elegí la opción raw → JSON para que Postman agregara automáticamente Content-Type: application/json. Si no lo pongo o lo envío en otro formato, el servidor podría devolverme un error (el anexo del taller menciona un 400) o interpretar mal los datos.

Fuentes:
- MDN, Content-Type: https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Content-Type
- MDN, Access-Control-Allow-Credentials: https://developer.mozilla.org/es/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials
- MDN Web Docs, *Date*: https://developer.mozilla.org/es/docs/Web/HTTP/Headers/Date

