# Dase de datos NoSQL Mongodb

Se utiliza Mongodb gracias a sus principales ventajas. Un  desarrollo ágil y escalable.
En esta mv está corriendo un contendor con imagen Mongodb. En tres pasos tienes configuración básica para usar Mongo:

1. Correr contenedor Mongodb.

```
$ docker run --name mongodb -d -p 27017:27017 mongo
```

2. Accedemos al contenedor mongodb para añadir un usuario

```
$ docker exec -it mongodb mongo admin
```

2. Añadir un usuario Mongo. Opcional
```
db.createUser({ user: 'darcusfenix', pwd: 'darcusfenix', roles: [ { role: "userAdminAnyDatabase", db: "cinema" } ] });
```

