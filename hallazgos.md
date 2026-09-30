# Hallazgos

## Tabla de peticiones

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
|---|---|---|---|---|
| 1 | GET /posts/1 | 200 Ok| 200 Ok | Si |
| 2 | GET /posts |200 Ok |200 Ok | Si |
| 3 | GET /posts/9999 |404 | 404 | Si|
| 4 | POST /posts | 201 | 201 | Si |
| 5 | PUT /posts/1 |200 | 200 | Si |
| 6 | PATCH /posts/1 |200 |200 | Si |
| 7 | DELETE /posts/1 | 200 |200 | Si |



## Tarea 4: GET de un recurso y de una colección

### Petición 1: GET /posts/1

- **Código de estado:** 200 OK
- **Cuántos elementos trae:** uno solo (un objeto entre llaves `{ }`)
- **Campos:** `userId`, `id`, `title` y `body`

### Petición 2: GET /posts

- **Código de estado:** 200 OK
- **Cuántos elementos trae:** 100 publicaciones (una lista entre corchetes `[ ]`; la última tiene el id 100)
- **Campos de cada elemento:** `userId`, `id`, `title` y `body`, los mismos que en la petición 1

### ¿En qué se diferencian los criterios de aceptación entre pedir un recurso y pedir una colección?

En el recurso verifico los datos de un elemento y en la colección verifico la forma de la lista ya sea la cantidad y esctrucutura repetida y otra diferencia es que digamos que la colección puede venir vaci [] y seguir siendo un 200 correcto, pero si yo pido un recurso que no  existe, lo correcto es un 404, como se ve en la peticion 3

## Tarea 5: error a propósito (GET /posts/9999)

Esperaba un 404 y obtuve un 404 Not Found; el cuerpo de la respuesta fue un objeto vacío `{}`. El caso de prueba **pasó**, porque el resultado obtenido coincide con el esperado. Pedí una publicación con un id que no existe y el servidor respondió correctamente que no la encontró.

**¿Qué pasaría si esa misma petición hubiera devuelto 200 con un cuerpo vacío? ¿Sería un defecto?**
Sí sería un defecto, porque esperaba un 404 (el id no existe) y habría obtenido un 200, así que el resultado difiere del esperado. Además, un 200 le indica al cliente que la petición funcionó, y en este caso eso sería falso.

## Tarea 6: POST cinco veces seguidas

Ejecuté el POST cinco veces seguidas y las cinco veces devolvió 201 Created con el mismo `id`: 101. En la petición 2, la última publicación tenía el id 100, así que el servidor asignó el siguiente número. Como siempre devolvió 101, deduzco que no guarda la publicación: si la guardara, esperaría un id distinto en cada envío (102 en el segundo).

**¿Cómo comprobaría, en una API real, que el recurso se creó de verdad?**

Para comprobar en una API real que el recurso se creó, haría un GET al id que devolvió el POST (por ejemplo, GET /posts/101). Si se guardó, esperaría un 200 con los datos que envié y ese id; si no, un 404.

## Tarea 7: PUT y PATCH

### Respuesta del PUT /posts/1

Cuerpo enviado:

```json
{
  "title": "Titulo corregido"
}
```

Respuesta (200 OK):

```json
{
  "title": "Titulo corregido",
  "id": 1
}
```

### Respuesta del PATCH /posts/1

Cuerpo enviado:

```json
{
  "title": "Titulo corregido"
}
```

Respuesta (200 OK):

```json
{
  "userId": 1,
  "id": 1,
  "title": "Titulo corregido",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

### Diferencia entre PUT y PATCH
La diferencia entre PUT y PATCH es que PUT lo que hace es que sobrescribe y borra lo que no se tenga en cuenta a la hora de la modificación, ya que haciendo la prueba vi que enviando el mismo cuerpo (solo con title) el PUT devolvio el id y el title y como no se tuvo en cuenta lo demás por eso a la hora de la respuesta los demás campos no aparecieron, pero a la hora de hacerlo con el PATCH pues me devolvio, userId, id, title y body, ya que lo que hace el PATCH es modificar algo en especifico y lo que no tengamos en cuenta pues lo deja intacto, por eso nos devolvio todo el cuerpo intacto meno el title que fue lo que modificamos.

### ¿Cuál usaría para corregir un error en un solo campo?

Para corregir un error en un solo campo usaria PATCH ya que me deja hacerlo poniendo especificamente lo que quiero cambiar como hicimos en la prueba, ya que existe el riesgo  de que si lo hacemos con PUT pues  se pierde lo demás.



### Peticion 7: DELETE
En el delete obtuve 200 Ok y el cuerpo fue un objeto vacio {}



## Tarea 10: valores límite

| id | Código obtenido |
|---|---|
| 99 | _200 Ok__ |
| 100 | 200 OK |
| 101 | 404 Not Found |


El id más alto que devuelve 200 es 100 y el primero que devuelve 404 es 101.
Este tipo de caso de prueba se llama valores limite , y los defectos se concentran ahí porque el comportamiento cambia justo en esa frontera, y ahi es onde los programadores más se equivocan ya que un  error típico es escribir < en vez de <= en una condicion (un error "por uno").


## Tarea 11: otros recursos y ruta anidada

### Recurso 1: GET /users

- **Código de estado:** 200 OK
- **Cuántos elementos trae:** 10
- **Campos:** `id`, `name`, `username`, `email` y `address`. Dentro de `address` hay `street`, `suite`, `city`, `zipcode` y `geo` (que a su vez tiene `lat` y `lng`).

### Recurso 2: GET /todos

- **Código de estado:** 200 OK
- **Cuántos elementos trae:** 200
- **Campos:** `userId`, `id`, `title` y `completed`.

### Ruta anidada: GET /posts/1/comments

- **Código de estado:** 200 OK
- **Cuántos comentarios trae:** id:5
- **Campos:** postId, id, name, email y body

### Cómo deduje la estructura de las URL
Se lee de izquierda a derecha, de lo general a lo específico. /posts es todas las publicaciones, /posts/1 es la publicación 1, y /posts/1/comments son los comentarios de esa publicación.
El campo postId lo confirma. En cada comentario, postId: 1 dice a qué publicación pertenece, y ese 1 es el mismo de la URL. O sea, la URL anidada muestra una relación que ya está en los datos.
Con todos pasa igual. Cada tarea trae userId, así que sigue el mismo patrón: las tareas del usuario 1 serían /users/1/todos. La guía oficial de JSONPlaceholder lista esa ruta entre las disponibles, y también dice que /posts/1/comments equivale a /comments?postId=1.
Lo que tienen en común todas las URL: empiezan con el nombre del recurso en plural (/posts, /users, /todos) y, si quieres uno solo, le agregas su id.


## Tarea 12: primera prueba automática

Código de la prueba: (el bloque pm.test con el 200)
Resultado con 200: verde (evidencias/05-test-automatico.png)
Resultado con 201: rojo (evidencias/05-test-automatico-rojo.png)
¿Por qué es importante ver fallar una prueba? Una prueba que siempre sale en verde no te dice nada, porque no sabes si de verdad comprueba algo o está mal escrita. Puede tener un error, o comprobar algo que siempre se cumple, y te daría una falsa seguridad. Al cambiar el 200 por 201, la respuesta real seguía siendo 200, así que la prueba detectó que no coincidía y se puso en rojo. Ahí demostraste que la prueba funciona y reacciona cuando algo está mal.

## Tarea 13: Pruebas automatizadas con scripts en Postman (pm.expect)

Para automatizar la validación de las respuestas HTTP, escribí tres pruebas personalizadas utilizando la sintaxis JavaScript de Postman (`pm.test` y `pm.expect`) en la pestaña **Scripts / After response** de la petición `GET https://jsonplaceholder.typicode.com/posts/1`.

### Código de las pruebas implementadas

```javascript
// Prueba 1: Verificar el tiempo de respuesta
pm.test("El tiempo de respuesta es menor a 1000 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});

// Prueba 2: Verificar la existencia de un campo en el JSON
pm.test("La respuesta contiene el campo 'title'", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('title');
});

// Prueba 3: Verificar el tipo de dato de un atributo
pm.test("El campo 'id' es de tipo numero", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.id).to.be.a('number');
});


Validación de rendimiento (responseTime): Comprueba que la latencia del servidor sea adecuada para una buena experiencia de usuario, verificando que el tiempo de respuesta no supere los 1000 milisegundos (en mis ejecuciones arrojó entre 75 ms y 230 ms).

Validación de la propiedad (to.have.property): Garantiza que la respuesta cumpla con la estructura esperada de la API al verificar que el JSON devuelto contenga explícitamente el campo title.

Validación del tipo de dato (to.be.a): Verifica que el valor asignado al campo id sea de tipo numérico y no una cadena de texto, previniendo errores de formateo en el desarrollo frontend.

Fuentes consultadas:

Postman Learning Center, Write scripts to test API responses: https://learning.postman.com/docs/writing-scripts/test-scripts/

Postman Learning Center, Postman JavaScript reference: https://learning.postman.com/docs/writing-scripts/script-references/postman-sandbox-api-reference/