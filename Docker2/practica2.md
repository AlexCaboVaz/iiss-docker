# Práctica 2 Docker

## Primera Parte
- Comenzamos la práctica creando un volumen Docker con el siguiente comando:
    
    ```
    docker volume create volumeDocker
    ```

- Tras este comando hemos creado un volumen siguiente los pasos del guión de practicas.
- Creamos el contenedor Nginx con el comando:

    ```
    docker run -d -p 80:8080 --name=ContenedorNginx --mount type=volume,source=volumeDocker,target=/app bitnami/apache
    ```

- Ya disponemos del contenedor, y tenemos añadido el volumen que habiamos creado con el primer comando, ademas de añadirle el puerto 80.
Para poder seguir con la práctica debemos de comprobar que el contenedor esta vacio y añadirle un saludo tal y como se nos pide.

    1. Accedemos a la terminal del contener:

        ```
        docker exec -it --user=root ContenedorNginx /bin/bash
        ```

    2. Y accedemos y modificamos el index.html (Hay que instalarlo en la terminal del contenedor).

        ```
        nano index.html
        ```

- Ya dentro del nano, debemos trabajar en el lenguaje HTML, y añadir lo sigueinte:

    ```
    <html>
        <head>
            <title>AlejandroCabo</title>
        </head>
        <body>
            <p>Realizado por Alejandro Cabo en 2023</p>
        </body>
    </html>
    ```

- Guardamos este fichero, con la ayuda de la guia que se nos da en la terminal, y tras ello, creamos un segundo contenedor, con el mismo comando del principio.

     ```
    docker run -d -p 81:8080 --name=ContenedorNginx --mount type=volume,source=volumeDocker,target=/app bitnami/apache
    ```

- Esta vez usamos el puerto 81, para diferenciarlo con el anterior. Al haber usado el mismo comando, con el mismo volumen pero diferente puerto, esto haria que copiaria en ambos lo que hay dentro del contenedor y lo podemos comprobar accediendo al localhost:80 y localhost:81.

![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker2/Captura%20desde%202023-05-21%2010-51-37.png)
![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker2/Captura%20desde%202023-05-21%2010-51-37.png)

## Segunda Parte

- Para esta segunda parte debemos crear una red y dos contenedores tal y como se nos pide en el guión

    1. Creamos la red

    ```
    docker network create redDocker
    ```

    2. Creamos el contenedor Ubuntu1 a la red.

    ```
    docker run -d -t -i --name Ubuntu1 --network redDocker ubuntu
    ```

    3. Hacemos lo mismo creando el segundo contenedor

    ```
    docker run -d -t -i --name Ubuntu2 ubuntu
    ```

- A continuacion con el mismo comando que utilziamos en la primera parte, accedemos a las terminales de los contenedores, consultado la ip y haciendo ping desde Ubuntu1 a Ubuntu2. Y comprobamos que no funciona.

![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker2/noping.png)
![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker2/p12.png)

- Que no funcione es debido aque Ubuntu2, no lo conectamos a la red, si os fijais no usamos el mismo comando que con ubuntu1, para eso debemos eliminar el contenedor Ubuntu2 y crearlo de nuevo.

    ```
    docker rm Ubuntu2
    ```

    ```
    docker run -d -t -i --name Ubuntu2 --network redDocker ubuntu
    ```

- Tras esto volvemos a realizar ping y vemos como ahira si se realiza, esto es debido a que ambos estan en la misma red.

![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker2/ping.png)
