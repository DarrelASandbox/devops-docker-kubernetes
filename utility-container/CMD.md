```sh
docker build -t node-util .

# Powershell command
docker run -it -v ${pwd}:/app node-util npm init -y
# MacOS/ Linux command
docker run -it -v $(pwd):/app node-util npm init -y

# ENTRYPOINT in dockerfile
# Powershell command
docker run -it -v ${pwd}:/app node-util i express
# MacOS/ Linux command
docker run -it -v $(pwd):/app node-util i express

# npm refers to npm in docker-compose.yaml
docker-compose run --rm npm init
```
