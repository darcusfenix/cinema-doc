# Arquitectura de los microservicios.

Vamos a empezar con la arquitectura utilizada en backend. 

Este es el diagrama que representa el diseño utilizado. Se trató de ser un poco más gráfico en cuanto al uso de las
tecnologías.

Los componentes que conforman este diseño son:

* Base de datos NoSQL Mongodb.
* Un clouster docker swarm.
* Un balanceador de carga.
* Un broker de mensajería.

Estos componentes están distribuidos en 5 máquinas virtuales, alojadas en Azure.

1. Máquina virtual dedicada a una instancia de Mongodb. 
2. Tres máquinas virtuales que complentan el clouster dedicado a microservicios rest-full.
3. Máquina virtual dedicada para el balanceador de carga hacia los microservicios.
4. Máquina virutal dedicada para el broker de mensajería y nginx. El broker se encuentra en un contenedor con imagen java.

## Mongodb

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

![alt text](https://www.dropbox.com/s/p8bzdssqik2tw9m/microservice-cinema-architecture.png?dl=1 "Microservices Architecture")

Ok, After of this users histories.