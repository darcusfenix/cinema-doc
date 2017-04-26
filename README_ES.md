# Proyecto galería de películas en un cine

Este es un proyecto que se intenta usar como portafolio. El cual, se prentende compartir un poco de conocimiento.

No es una arquitectura perfecta, pero se espera que te dé una idea de cómo diseñar tu propia.

Basicamente, es una arquitectura basada en microservicios contenerizada en docker bajo el clouster docker swarm.

Este ejemplo de arquitectura es end-to-end, es decir, se mostrará el desarrollo, código y ejemplo de cada uno de los componentes
que lo conforman. Desde la interacción del usuario hasta la base de datos. Y para ello se dividio en dos. Una parte es 
backend y otra para frontend.

Se plantearon cuatro historias de usuario para definir esta arquitectura. Los cuales son:

1. Como un Usuario, Yo quiero ver todas las películas en la galería.
2. Como un Usuario, Yo quiero ver todos los comentarios de una película, para que yo pueda saber las criticas de los demás usuarios.
3. Como un Usuario, Yo quiero añadir un comentario a una película, para que yo pueda dar mi critica de la misma.
4. Como un Usuario, Yo quiero recibir las nuevas películas en la galería, para que yo puedar ver la última sin actualizar la página.

Las siguientes imágenes son el resultado final (Single page application) que el usuario podrá interactuar.
    
Captura de pantalla de la galería de películas.

![alt text](https://www.dropbox.com/s/p9n9zn7cugicknk/spa-movies.png?dl=1 "Single page application - Movies")

Captura de pantalla de los comnetarios y formulario para añadir uno más a la película.

![alt text](https://www.dropbox.com/s/w4yg9h3bx9myhdr/spa-comments-of-a-movie.png?dl=1 "Single page application - Movies")


Juan Crisóstomo