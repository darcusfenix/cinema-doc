# Servicio rest-full Películas


De las 4 historias de usuario en este componente se atienden dos, la primera y cuarta us* .

Los servicios rest se desarrollaron con Nodejs y Express. En el proyecto se expone un endpoint relacionado
con las películas. Se realizan las operaciones CRUD.


| endpoint     | verbo http     | descripción                     |
|--------------|----------------|---------------------------------|
|  /movies     | post           | Crea una nueva película [1]  |
|  /movies     | get            | Retorna un array de películas  |
|  /movies/:id | get            | Retorna un objeto película por identificador  |
|  /movies/:id | put            | Cambia el valor de todos los atributos de la película  |
|  /movies/:id | patch          | Cambia el valor de solo los atributos envíados como datos de parámetros  |
|  /movies/:id | delete         | Elimina el registro de la película  |


Una vez desarrollado las operaciones crud se creó una imagen docker que expone el puerto 3000.

* User history

[1] Cuando una película es guardada en la colección movies de mongo y no hubo error se conecta al broker 
de mensajería y el identificador de la nueva película se envía como mensaje al tópico "movies".
