# baseImage
FROM node

WORKDIR /app

# npm i will not run again because we copy our source code
# The layers that will run again will start from COPY . ./
COPY package.json /app

RUN npm install

# First path is outside of the container/ image
# Same folder as the dockerfile
# Host file system
# Second path is inside of the image
# Image/ container file system
# ./ is a relative path that points at WORKDIR /app

# The package.json file is copied again but that doesn't matter.
# We ran npm install before we copied everything, that's the important thing here.
COPY . ./

# For localhost:3000
EXPOSE 3000

# CMD will not run when the image is created but
# when a container is started
CMD ["node", "server.js"]