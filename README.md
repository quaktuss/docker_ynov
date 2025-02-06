
 ## Exécuter un serveur web (apache, nginx, …) dans un conteneur docker

```
$ docker pull nginx
$ docker image ls
$ echo "Hello World" >> html/index.html
$ docker run --name mathieu-nginx -v ./html/:/usr/share/nginx/html:ro -p 80:80 -d nginx
$ docker rm -f mathieu-nginx
$ docker run --name mathieu-nginx -p 80:80 -d nginx
$ docker cp ./html/index.html mathieu-nginx:/usr/share/nginx/html/index.html

```

## Builder une image
```
$ touch Dockerfile
$ docker built -t mynginx .
$ docker run --name mathieu-nginx -p 80:80 -d my-nginx
$ docker rm -f mathieu-nginx
```

La difference avec l'exercice précédent, est qu'il est moins fastidieux de créer un Dockerfile que de faire avec Docker CLI, qui peut comporter des erreurs.

L'inconvenient de la partie Dockerfile est qu'une modification prends plus de temps que en CLI

## Utiliser une base de données dans un conteneur docker