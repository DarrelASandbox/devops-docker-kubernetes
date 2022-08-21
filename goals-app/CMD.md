```sh
# DB
docker run --name mongodb --rm -dp 27017:27017 mongo

# Backend
docker build -t goals-app-backend .
docker run --name goals-app-backend --rm -dp 80:80 goals-app-backend

# Frontend
docker build -t goals-app-frontend .
docker run --name goals-app-frontend --rm -dp 3000:3000 goals-app-frontend


###############################################################################


# Network
docker network create goals-network
docker run --name mongodb --rm -d --network goals-network mongo

# Double check if the connection is to mongodb (container name) at app.js (backend folder)
docker run --name goals-app-backend --rm -d --network goals-network goals-app-backend

# Double check if proxy is setup in package.json for frontend and amend App.js (src) accordingly
docker run --name goals-app-frontend --rm -dp 3000:3000 --network goals-network goals-app-frontend

# Volume (Persist data)
# Assign a name and map the path inside of the container
docker run --name mongodb --rm -d -v data:/data/db --network goals-network mongo

# Authentication
# Delete the old volume for the database, if that volume was created without passing the credentials before.
docker run --name mongodb --rm -d -v data:/data/db --network goals-network -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo


###############################################################################


# Explore container folders
# interactive and tty flags
# Ctrl + D to exit
docker exec -it goals-app-backend /bin/bash
ls -lsa

# Volume for the log file using bind mount
# Ensure you are in the correct directory for pwd to work
# Anonymous volume for node_modules so that the folder persists and not overwritten by non-existing node-modules folder
# Powershell command
docker run --name goals-app-backend --rm -d -v ${pwd}:/backend -v logs:/backend/logs -v /backend/node_modules --network goals-network goals-app-backend
# MacOS/ Linux command
docker run --name goals-app-backend --rm -d -v $(pwd):/backend -v logs:/backend/logs -v /backend/node_modules --network goals-network goals-app-backend

# After nodemon setup
docker logs goals-app-backend

# Blind mount for frontend
# Powershell command
docker run --name goals-app-frontend --rm -dp 3000:3000 -v ${pwd}/src:/frontend/src --network goals-network goals-app-frontend
# MacOS/ Linux command
docker run --name goals-app-frontend --rm -dp 3000:3000 -v $(pwd)/src:/frontend/src --network goals-network goals-app-frontend
```
