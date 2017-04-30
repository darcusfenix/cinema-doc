# Arquitectura de los microservicios.

![alt text](https://www.dropbox.com/s/p8bzdssqik2tw9m/microservice-cinema-architecture.png?dl=1 "Microservices Architecture")

Vamos a empezar con la arquitectura utilizada en backend. 

Este es el diagrama que representa el diseño utilizado. Se trató de ser un poco más gráfico en cuanto al uso de las
tecnologías.

Los componentes que conforman este diseño son:

* Base de datos NoSQL Mongodb.
* Un clouster docker swarm.
* Un balanceador de carga.
* Un broker de mensajería.

Estos componentes están distribuidos en 6 máquinas virtuales, alojadas en Azure.

1. Máquina virtual dedicada a una instancia de Mongodb. 
2. Tres máquinas virtuales que complentan el clouster dedicado a microservicios rest-full.
3. Máquina virtual dedicada para el balanceador de carga hacia los microservicios.
4. Máquina virutal dedicada para el broker de mensajería y nginx. El broker se encuentra en un contenedor con imagen java.
