# Diseño de microservicios.



![alt text](https://www.dropbox.com/s/expp2z74rz0w9cn/cInema-projects.png?dl=1 "Microservices Architecture")

Para el desarrollo de estos componentes que exponen los servicios rest se diseñó una arquitectura de proyectos en tres por separado. Uno
"microservice-cinema-movies" que únicamente atiende las operaciones de películas y "microservice-cinema-comments" que 
 sólo atiende operaciones de comentarios. Siguiendo los principios de un microservicio. Estos dos proyectos tienen como 
 dependencia el proyecto "microservice-cinema-core". En este último sólo contiene:
 
 * Modelos de mongo, Movie y Comment.
 ```javascript
 import mongoose from "mongoose";
 
 const Schema = mongoose.Schema,
     commentSchema = new Schema({
         "title": {
             "type": String,
             "required": true,
         },
         "message": {
             "type": String,
             "required": true,
         },
         "date": {
             "type": Date,
             "required": true,
             "default": new Date()
         },
         "rate": {
             "type": Number,
             "default": 0
         },
         "active": {
             "type": Boolean,
             "default": true
         },
         "movie": {
             "type": Schema.Types.ObjectId,
             "ref": "movie",
             "required": true,
         }
     });
 
 export default commentSchema;
```
 * Variables en común.
 ```javascript
 export const settings = {
     "nameServer": "localhost",
     "mongodbUrl": process.env.MONGODB_URL ? process.env.MONGODB_URL : "localhost",
     "mongodbDatabase": process.env.MONGODB_DATABASE ? process.env.MONGODB_DATABASE : "cinema",
     "mongodbUser": process.env.MONGODB_USER ? process.env.MONGODB_USER : null,
     "mongodbPassword": process.env.MONGODB_PASSWORD ? process.env.MONGODB_PASSWORD : null,
     "mongodbPort": process.env.MONGODB_PORT ? process.env.MONGODB_PORT : 27017,
     "expressPort": process.env.EXPRESS_PORT ? process.env.EXPRESS_PORT : 3000,
     "activemqUrl": process.env.ACTIVEMQ_URL ? process.env.ACTIVEMQ_URL : "tcp://activemq.crisostomo.soy",
     "activemqPort": process.env.ACTIVEMQ_PORT ? process.env.ACTIVEMQ_PORT : 1883,
     "activemqContext": process.env.ACTIVEMQ_CONTEXT ? process.env.ACTIVEMQ_CONTEXT : "mqtt",
     "moviesTopic": process.env.MOVIES_TOPIC ? process.env.MOVIES_TOPIC : "movies",
     "commentsTopic": process.env.MOVIES_COMMENTS ? process.env.MOVIES_COMMENTS : "comments",
     "cache": {
         "password": "bfdf8aba8e784557af145db15f8703c1"
     },
     "session": {
         "password": "1652f8dfa00443589e12afb7ec37f2c5"
     }
 };
 ```
 * Módulo que crea conexión con Mongo.
 ```javascript
 return new Promise((resolve, reject) => {
         const address = `mongodb://${settings.mongodbUser !== null ? settings.mongodbUser + ':' : ""}${settings.mongodbPassword !== null ? settings.mongodbPassword + '@' : ""}${settings.mongodbUrl}:${settings.mongodbPort}/${settings.mongodbDatabase}`;
         log.debug("address to mongodb: ", address);
         if (!internalConnectionPool[address]) {
 
             try {
 
                 const conn = mongoose.createConnection(address, opts);
                 conn.on("open", () => {
 
                     internalConnectionPool[address] = conn;
                     resolve(internalConnectionPool[address]);
 
                 });
 
                 conn.on("error", (err) => {
 
                     log.error("MongoDB error: ");
                     log.error(err);
 
                 });
 
             } catch (err) {
 
                 reject(err);
 
             }
 
         } else {
 
             return resolve(internalConnectionPool[address]);
 
         }
 
     });
 ```
 * Factories de los modelos.
 ```javascript
 import MovieModel from "../models/MovieModel";
 import connectionProvider from "../dataAccess/connectionProvider";
 
 export const getMovieModel = async function() {
     try {
 
         const conn = await connectionProvider();
         return conn.model("movie", MovieModel);
 
     } catch (err) {
 
         throw err;
 
     }
 
 };

 ```
 * Módulo que conecta con el message broker.
 ```javascript

 
     const {activemqUrl, activemqPort, activemqContext} = settings;
     const url = `${activemqUrl}:${activemqPort}/${activemqContext}`;
 
     if (typeof message === "object") {
 
         message = message.toString();
 
     }
 
     log.debug({"topic": topic, "message": message, "url": url});
 
     return new Promise((resolve, reject) => {
 
         client = mqtt.connect(url);
         client.on("connect", () => {
 
             client.publish(topic, message, null, (err) => {
 
                 if (err) {
 
                     log.error(err);
                     reject(0);
 
                 }
 
                 client.end();
                 resolve(1);
 
             });
 
         });
 
         client.on("error", () => {
 
             reject(0);
 
         });
 
     });
 

 ```
 

 