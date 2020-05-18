# Comandos básicos de Docker para el curso

## Ver contenedores en ejecución
docker ps

## Ver todos los contenedores
docker ps -all

## Ver imágenes
docker image list

## Crear una imagen
docker build --tag <IMAGE_NAME> <ruta de la carpeta donde esta el fichero Dockerbuild>

## Crear un contenedor desde una imagen
docker container create --name <CONTAINER_NAME> <IMAGE_NAME>

## Iniciar contenedor
docker start <CONTAINER_NAME>

## Acceso a una shell en el contenedor
docker exec -it <CONTAINER_NAME> <bash/sh>

## Propiedades de un contenedor
docker inspect <CONTAINER_NAME>

## Parar un contenedor
docker stop <CONTAINER_NAME>

## Borrar un contenedor
docker rm <CONTAINER_NAME>

## Borrar una imagen
docker rmi <IMAGE_NAME>

## Borra todo y dejar docker limpio
docker system prune --all --force --volumes
