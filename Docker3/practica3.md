# Práctica 3
## Primer Ejercicio

- Lo primero que debemos hacer es crear un fichero docker-compose.yml que use Drupal y MySQL.
    ```
    version: '3.1'

    services:
    db:
        image: mysql:5.7
        volumes:
        - volumenDocker:/var/lib/mysql
        environment:
        MYSQL_ROOT_PASSWORD: iiss
    drupal:
        image: drupal:9-apache
        ports:
        - "81:80"
        volumes:
        - volumenDocker:/var/www/html
        environment:
        DRUPAL_DATABASE_HOST: db
        DRUPAL_DATABASE_NAME: drupal
        DRUPAL_DATABASE_USER: drupal
        DRUPAL_DATABASE_PASSWORD: iiss

    volumes:
    volumenDocker:
  ```

- Con esa configuracion hemos creado un fichero docker compose, en el cual detallamos lo que se nos ha pedido en el guión de practicas. A continuación, ejecutamos.

    ```
    sudo docker-compose up
    ```

- Si ahora, al igual que en practicas anteriores accedemos a LocalHost:81 podemos comprobar que nos sale la siguiente imagen:

    ![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker3/primera.png)


## Segundo Ejercicio

- En este apartado debemos de realizar practicamente lo mismo que en el anterior, simplemente usando wordpress y mariadb

    ```
    version: "3"

    services:

    wordpress:
    image: bitnami/wordpress:latest
    container_name: wordpress_
    environment:
        - ALLOW_EMPTY_PASSWORD=yes
        - WORDPRESS_DATABASE_USER=bn_wordpress
        - WORDPRESS_DATABASE_NAME=bitnami_wordpress
    ports:
        - 82:8080
    networks:
        - redDockerC
    
    mariadb:
    image: bitnami/mariadb:latest
    container_name: mariadb
    environment:
        - ALLOW_EMPTY_PASSWORD=yes
        - MARIADB_USER=bn_wordpress
        - MARIADB_DATABASE=bitnami_wordpress
    networks:
        - redDockerC

    networks:
    redDockerC:
    ```

- El fichero contiene tanto wordpress como mariadb, hemos conectado el puerto 82 con el wordpress y a la red, siguiendo el guión. Por ultimo, si volvemos a ejecutar de la misma forma que antes con el comando up, y entramos en LocalHost:82, nos encontramos la siguiente imagen:

    ![Image text](https://github.com/AlexCaboVaz/iiss-docker/blob/main/Docker3/segunda.png)


