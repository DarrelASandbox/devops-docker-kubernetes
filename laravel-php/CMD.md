```sh
# Might want to empty src folder first
# run individual container of docker-compose.yaml
docker-compose run --rm composer create-project --prefer-dist laravel/laravel=8 .

# Update as below for the .env file in the src folder
########################
  DB_CONNECTION=mysql
  DB_HOST=mysql
  DB_PORT=3306
  DB_DATABASE=homestead
  DB_USERNAME=homestead
  DB_PASSWORD=secret
########################

docker-compose up -d
docker-compose down

# forces docker to rebuild if there is any changes
docker-compose up -d --build server

docker-compose run --rm artisan migrate
```
