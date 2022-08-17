```sh

# node-app
cd node-app
docker build -t node-app:1 .
docker run -p 3000:3000 -d --rm --name node-app c97eb1efa7cf
# If --rm flag is not used
docker start node-app

# python-app
cd python-app
docker build -t python-app:1 .
docker run -it --rm --name python-app 9755cab4914f
# If --rm flag is not used
docker start -ai python-app

```
