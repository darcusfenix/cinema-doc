# Dase de datos NoSQL Mongodb

![alt text](https://www.dropbox.com/s/6jh8nwy9q8vhma4/mongodb.png?dl=1 "Microservices Architecture")

Se utiliza Mongodb gracias a sus principales ventajas. Un  desarrollo ágil y escalable.
En esta mv está corriendo un contendor con imagen Mongodb. En 3 paso tienes una configuración básica para usar Mongo:

* Correr contenedor Mongodb.

```
$ docker run --name mongodb -d -p 27017:27017 mongo
```

* Accedemos al contenedor mongodb para añadir un usuario

```
$ docker exec -it mongodb mongo admin
```

* Añadir un usuario Mongo. Opcional
```
db.createUser({ user: 'darcusfenix', pwd: 'darcusfenix', roles: [ { role: "userAdminAnyDatabase", db: "cinema" } ] });
```

