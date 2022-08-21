```sh
cd rng
docker build .
# -i flag is interactive
# -t flag gives a terminal
docker run -it 2030

# Starts in detach mode
# which means terminal cannot accept STDIN
# We do not want to do this
docker start eager_burnell

# Do this instead
docker start -ai eager_burnell

##############################################################

# Delete images & containers
docker rm CONTAINER CONTAINER CONTAINER

# Show a list of images
docker images
# rmi: remove images
docker rmi IMAGEID IMAGEID IMAGEID
# Remove all unused images
docker image prune
# Remove image after running
docker run -p 3000:3000 -d --rm 82ef923ea973

##############################################################

# See image information such as layers
docker image inspect 82ef923

# Create a test.txt file in dummy folder
# Copy everything from dummy folder into CONTAINER
docker cp dummy/. eager_burnell:/test

# Delete test.txt file
# Copy everything from CONTAINER folder into dummy folder
# Good when you need to pull files out of a container
# Files for analytics or debugging
docker cp eager_burnell:/test dummy
```
