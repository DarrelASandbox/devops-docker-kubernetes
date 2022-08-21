```sh
docker build -t favorite .
docker run --name favorite --rm -dp 3000:3000 favorite

# Mongo image from docker hub
# mongodb://host.docker.internal:27017/swfavorites (LocalHost)
docker run -d --name mongodb mongo

# Check IPAddress of container
# mongodb://172.17.0.2:27017/swfavorites (Container)
docker container inspect mongodb

# mongodb://mongodb:27017/swfavorites (Container)
docker container prune
docker run -d --name mongodb --network fav-network mongo
docker network create fav-network
# Do not need -p flag to publish any port
# It is only require if we want to connect to something in the container from our localhost machine
# or from outside the container network
# In this case we are connecting container to container via a network we have created
docker run --name favorite --network fav-network --rm -d 3000:3000 favorite
docker logs favorite
```
