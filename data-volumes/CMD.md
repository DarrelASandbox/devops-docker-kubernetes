```sh
# Volume commands
docker volume --help

docker build -t feedback-app .
docker run -p 3000:80 -d --name feedback-app --rm feedback-app
docker logs feedback-app
docker stop feedback-app

# Remove container but Name volume will persist
docker run -dp 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback-app

# Bind Mounts so that we can edit the html file without rebuilding image
# Powershell command
docker run -dp 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v ${pwd}:/app -v /app/node_modules feedback-app
# MacOS/ Linux command
docker run -dp 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v $(pwd):/app -v /app/node_modules feedback-app

# .env file variables
docker run -dp 3000:8000 --env-file ./.env --rm --name feedback-app -v feedback:/app/feedback -v ${pwd}:/app -v /app/node_modules feedback-app

# Build image on a different tag on a different arg value
docker build -t feedback-app:dev --build-arg DEFAULT_PORT=8000 .
```
