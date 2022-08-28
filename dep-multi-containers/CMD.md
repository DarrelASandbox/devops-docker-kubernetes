```sh
# Backend for Docker Hub
docker build -t dep-multi-containers ./backend
docker tag dep-multi-containers darrela/dep-multi-containers
docker push darrela/dep-multi-containers

# Frontend for Docker Hub
#-f flag lets user specify the Dockerfile name
docker build -f frontend/Dockerfile.prod -t darrela/dep-multi-containers-client ./frontend
docker push darrela/dep-multi-containers-client
```
