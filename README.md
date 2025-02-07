
 ## Exécuter un serveur web (apache, nginx, …) dans un conteneur docker

```bash
$ docker pull nginx
$ docker image ls
$ echo "Hello World" >> html/index.html
$ docker run --name mathieu-nginx -v ./html/:/usr/share/nginx/html:ro -p 80:80 -d nginx
$ docker rm -f mathieu-nginx
$ docker run --name mathieu-nginx -p 80:80 -d nginx
$ docker cp ./html/index.html mathieu-nginx:/usr/share/nginx/html/index.html

```

## Builder une image
```bash
$ touch Dockerfile
$ docker built -t mynginx .
$ docker run --name mathieu-nginx -p 80:80 -d my-nginx
$ docker rm -f mathieu-nginx
```

La difference avec l'exercice précédent, est qu'il est moins fastidieux de créer un Dockerfile que de faire avec Docker CLI, qui peut comporter des erreurs.

L'inconvenient de la partie Dockerfile est qu'une modification prends plus de temps que en CLI

## Utiliser une base de données dans un conteneur docker
```bash
$ docker run --name mysql-server -e MYSQL_ROOT_PASSWORD=mypassword -d mysql:5.7

$ docker run --name phpmyadmin-container --link mysql-container:db -p 8080:80 -d phpmyadmin

```

## Faire la même chose que précédemment en utilisant un fichier docker-compose.yml

Le `docker-compose.yml` apporte une simplicité dans la chose, car en un fichier, on peut créer tout ce qu'on veut et modifié à notre guise.

Les variables environnement permettent en plus de configurer plus profondément mysql.

```yaml
services:
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: 'mypassword'
  myadmin:
    image: phpmyadmin
    ports:
      - 80:80
    environment:
      PMA_HOST: mysql
```


## Observation de l’isolation réseau entre 3 conteneurs
```yaml
services:
  web:
    image: praqma/network-multitool
    container_name: web
    networks:
      - frontend

  app:
    image: praqma/network-multitool
    container_name: app
    networks:
      - frontend
      - backend

  db:
    image: praqma/network-multitool
    container_name: db
    networks:
      - backend

networks:
  frontend:
  backend:
```