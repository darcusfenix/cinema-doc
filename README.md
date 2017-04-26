# Cinema gallery project

This is a project that I intend to use as a portfolio. In which I want to share some of my knowledge.

Basically it is an architecture based on microservices containerized in docker under a clouster docker swarm.

Mongodb is the database that each container connects to.

For push notifications I am using the Activemq messaging broker that exposes two ports, one for websocket and tcp for the containers. Mqtt is the protocol used for communication.

I use a load balancer for the rest-full services and another for the spa.

For the front-ent part I developed a single page application in react js / redux.

This spa consumes the movies and shows in gallery. In each movie we can see its image, description and comments. If we want we can add one to the selected movie.

When the main component of the spa is rendered, start the connection via websocket to the message broker.

If the connection to the websocket was successful the spa subscribes to two topics. One to receive notifications of new comments and another for new movies.

When a new movie notification is received the spa performs the request to obtain the entire object of the movie. And, to finish if the answer of the movie is successful it paints as first element the new film in the gallery.

    
Screenshot of the gallery of movies

![alt text](https://www.dropbox.com/s/p9n9zn7cugicknk/spa-movies.png?dl=1 "Single page application - Movies")

Screenshot of the movie's comments

![alt text](https://www.dropbox.com/s/w4yg9h3bx9myhdr/spa-comments-of-a-movie.png?dl=1 "Single page application - Movies")


Juan Crisóstomo