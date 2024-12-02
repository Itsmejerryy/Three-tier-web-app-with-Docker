# Docker_Hub_Demo
Repo for the Docker Hub [Demo Video](https://www.youtube.com/watch?v=voEiMbX1cuQ).

# I encountered errors as I use windows OS so I modify the original ordering of commands as well as app-server Dockerfile due to fix the errors.

## Commands
- Note: USERNAME and PASSWORD hard-coded for Demo Purposes!

### Pull Mongo image
```
docker pull mongo
```
### Pull Mongo-Express image
```
docker pull mongo-express
```
### Create Volume
```
docker volume create app-volume
```

### Run Mongo Container (note for mounted volume)
```
docker container run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=password --network app-network --mount source=app-volume,target=/data/db --name mongo mongo
```

### Run Mongo-Express Container
```
docker container run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=root -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongo --network app-network --name mongo-express mongo-express
```


### Build app-server Image
```
docker build -t app-server -f ./src/app-server/Dockerfile .
```

### Run app-server Container
```
docker container run -it -d -p 3000:3000 --network app-network --name app-server app-server
```

### Build web-server Image
```
docker build -t web-server -f ./src/web-server/Dockerfile .
```

### Run web-server Container
```
docker run -it -d -p 80:80 --network app-network --name web-server web-server
```

### Push Images to Docker hub
```
docker image build -t itsmejerry/app-server:1.0 -f ./src/app-server/Dockerfile .
docker image push itsmejerry/app-server:1.0

docker image build -t itsmejerry/web-server:1.0 -f ./src/web-server/Dockerfile .
docker image push itsmejerry/web-server:1.0
```

### Run Docker Compose
```
docker compose -f .\src\docker-compose.yaml up  
```
# Three-tier-web-app-with-Docker
