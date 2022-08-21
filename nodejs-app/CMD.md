```sh
cd nodejs-app
docker build .
docker run -p 3000:3000 fb02
docker ps
docker stop magical_engelbart

# Rebuild after amending files in nodejs-app folder
docker build .
docker run -p 3000:3000 f244

# Restart container
docker ps -a
docker start youthful_hermann

# start in attach mode
docker start -a youthful_hermann

# By default, if you run a Container without -d, you run in "attached mode".
# If you started a container in detached mode (i.e. with -d),
# you can still attach to it afterwards without restarting the Container with the following command:
docker attach CONTAINER
# attaches you to a running Container with an ID or name of CONTAINER

# Custom container name
# Localhost 3000 on docker port 80
docker run -p 3000:80 -d --rm --name nodejs-app f24419

# Specific image tag (tag can be a number of string)
docker build -t goals:latest.
```
