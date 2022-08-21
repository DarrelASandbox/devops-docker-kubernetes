```sh
# DB
docker run --name mongodb --rm -dp 27017:27017 mongo

# Backend
docker build -t goals-app-backend .
docker run --name goals-app-backend --rm -dp 80:80 goals-app-backend

# Frontend
docker build -t goals-app-frontend .
docker run --name goals-app-frontend --rm -dp 3000:3000 goals-app-frontend
```
