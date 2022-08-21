```sh
# dockerfile
docker build .

# p flag publish on port 3000:3000 image id then visit localhost:3000
docker run -p 3000:3000 9134b990094eade5b78a511f9d423cb86736886a88c55426324b4da334c2ffea

# List all running containers
# docker processes
docker ps
# Stop NAME of container
docker stop elegant_ganguly
```
