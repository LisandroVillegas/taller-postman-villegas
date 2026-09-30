## Tarea 8: Idempotencia

**Qué es:** Un método es idempotente si repetir la misma petición varias veces deja al servidor en el mismo estado que hacerla una sola vez. La primera vez sí puede cambiar algo las repeticiones ya no  cambian nada más, por ejemplo pulsar el botón del ascensor cinco veces equivale a pulsarlo una  y en cambio dar "Pagar" cinco veces puede generar 5 cobros. 

Fuente: https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Methods/PUT

**Cuáles lo son:** GET es idempotente porque solo lee, no cambia nada. PUT también es idempotente porque reemplaza el recurso porque lo envías, repetirlo deja el mismo resultado. DELETE también es idempotente porque despues de borrar, el recurso ya no existe y borrar de nuevo no cambia el estado (aunque la segunda vez puede dar 404), POST no lo es ya que cada envio puede crear un recurso nuevo y PATCH depende de la modificación aunque MDN lo marca como "NO", ahi en la documentación o bueno en el link de la fuente se puede ver en las tablas.

**Lo que observé en Postman:**
- PUT enviado tres veces: La primera vez pues el PUT si dejó el recurso con el titulo nuevo pero al darle 3 veces más pude notar que no cambió el resultado, el estado quedó igual que después del primer envio, entonces eso es ser idempotente.

- POST enviado cinco veces: siempre devolvió 201 con id 101 ya que JSONPlaceholder solo simula la creación y no guarda nada, por eso el id nunca avanza a 102 o 103 y asi sucesivamente. Lo que pasaria en una API real es que cada POST crearia un recurso nuevo con un id distinto, por eso el POST no es idempotente, ya que repetirlo cambia el estado del servidor.