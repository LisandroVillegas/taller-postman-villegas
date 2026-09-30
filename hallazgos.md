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
