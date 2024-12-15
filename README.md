# THIS IS THE SECOND PART
### The second part of this project is available [@Gitlab](https://www.youtube.com/watch?v=voEiMbX1cuQ). I leveraged gitlab's CICD pipeline to deploy the containerized microservices to a remote server automatically. I chose the more extended method by using the Dockerfile to better understand the processes. 

## Results:

build images and store them in the GitLab container registry
![image](https://github.com/user-attachments/assets/b3084989-b4c3-4efe-9fb0-ec2c87f1bf34)

Successful execution of the jobs
![image](https://github.com/user-attachments/assets/ddb85cdc-c7d3-4fce-a2a5-4abc39a6973a)

mongo express
![image](https://github.com/user-attachments/assets/9f9e312e-943d-40b8-a167-4d6d8fda2016)

app server
<br>![image](https://github.com/user-attachments/assets/f3b4d778-0105-4248-b5a4-7cf203781d1e)

web server
<br>![image](https://github.com/user-attachments/assets/95a388a4-214c-477c-9016-280f72a8bef9)


-------------------------------------------------------------------------------------------------------------

# THIS IS THE FIRST PART
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
