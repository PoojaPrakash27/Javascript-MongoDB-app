

https://www.youtube.com/watch?v=6YisG2GcXaw&list=PLy7NrYWoggjwPggqtFsI_zMAwvG0SqYCb&index=8


https://gitlab.com/nanuchi/techworld-js-docker-demo-app

docker run postgres:9.6

Status: Downloaded newer image for postgres:9.6
Error: Database is uninitialized and superuser password is not specified.
       You must specify POSTGRES_PASSWORD to a non-empty value for the
       superuser. For example, "-e POSTGRES_PASSWORD=password" on "docker run".

       You may also use "POSTGRES_HOST_AUTH_METHOD=trust" to allow all
       connections without a password. This is *not* recommended.

       See PostgreSQL documentation about "trust":
       https://www.postgresql.org/docs/current/auth-trust.html
(base)  ✘ ✝  ~/workspaces/docker-compose-tutorial-nana 


 docker run -e POSTRES_PASSWORD=postgres -e POSTGRES_USER=postgres -e POSTGRES_HOST_AUTH_METHOD=trust  postgres:9.6

-p HOST_PORT:CONTAINER_PORT

docker run -p6000:6379 redis

Creage a NEW container:

docker run ...

Restart a stopped container (retains previous properties):

docker start ...



https://gitlab.com/nanuchi/techworld-js-docker-demo-app

https://hub.docker.com/_/mongo

 docker run -d --network some-network --name some-mongo \
	-e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
	-e MONGO_INITDB_ROOT_PASSWORD=secret \
	mongo

$ docker run -it --rm --network some-network mongo \
	mongo --host some-mongo \
		-u mongoadmin \
		-p secret \
		--authenticationDatabase admin \
		some-db
> db.getName();
some-db


Commands for app

docker network create mongo-network

docker run -d \ 
-p 27017:27017 \
--network mongo-network \ 
--name mongodb \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
mongo

docker run -d \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
--net mongo-network \
--name mongo-express \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express

Docker compose version of above:

version: '3'
services:
  mongodb:
    image: mongodb
    ports:
    - 27017:27017
    environment:
    - MONGO_INITDB_ROOT_USERNAME=admin
    - MONGO_INITDB_ROOT_PASSWORD=password
  mongo-express:
    image: mongo-express
    ports:
    - 8081:8081
    environment:
    - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
    - ME_CONFIG_MONGODB_ADMINPASSWORD=password
    - ME_CONFIG_MONGODB_SERVER=mongodb


save as mongo.yaml

docker compose -f mongo.yaml up

## Lesson 10
https://www.youtube.com/watch?v=WmcdMiyqfZs&list=PLy7NrYWoggjwPggqtFsI_zMAwvG0SqYCb&index=10


### Image Environment Blueprint

install node

set MONGO_DB_USERNAME=admin

set MONGO_DB_PASSWORD=password

create /home/app folder

copy current files to /home/app folder

CMD: executes an entry point linux command

### Dockerfile

We will define env variables in the dockerfile, but it is probably better to define them in the docker-compose.yml file so you could change them later.

COPY command executes on the host!  RUN executes in the container.

CMD: execute an entry point Linux command.  You can have multiple RUN commands but only one CMD command.

The file must ALWAYS be named Dockerfile.

```Dockerfile
FROM node:13-alpine

ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PASSWORD=password

RUN mkdir -p /home/app

COPY . /home/app

CMD ["node", "/home/app/server.js"]
```

docker build -t my-app:1.0 .

docker run my-app:1.0

Re-build the container after changing the Dockerfile.  But first delete the old image, which might require deleting the  (possibly stopped) container first.

Get the container ID:

docker ps -a | grep my-app

Delete the container:

docker rm [CONTAINER_ID]

Delete the image:

docker rmi [IMAGE_ID]

Re-build the image:

docker build -t my-app:1.0 .

Run the image/container:

docker run my-app:1.0

docker exec -it [CONTAINER_ID] /bin/sh

Check for environment variables:

env





