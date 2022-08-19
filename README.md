## About The Project

- Docker & Kubernetes: The Practical Guide [2022 Edition]
- Learn Docker, Docker Compose, Multi-Container Projects, Deployment and all about Kubernetes from the ground up!
- [Maximilian Schwarzmüller](https://github.com/maxschwarzmueller)
- [Academind](https://academind.com/)

&nbsp;

## Commands

```sh
# dockerfile
docker build .

# p flag publish on port 3000:3000 image id then visit localhost:3000
docker run -p 3000:3000 9134b990094eade5b78a511f9d423cb86736886a88c55426324b4da334c2ffea

# List all running containers
# docker processes
docker ps
# Stop NAME of container
docker stop elegant_ganguly

##############################################################

# nodejs-app folder
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

##############################################################

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

##############################################################

# Custom container name
# Localhost 3000 on docker port 80
docker run -p 3000:80 -d --rm --name nodejs-app f24419

# Specific image tag (tag can be a number of string)
docker build -t goals:latest.

# Volume commands
docker volume --help
```

&nbsp;

---

&nbsp;

## Basics

- [Docker](https://www.docker.com/) is a container technology: A tool for creating and managing containers.
  - <b>Environment: </b> The runtimes, languages & frameworks
  - Development environment and production environment are often not the same
- <b>Virtual Machines</b>

|                               Pro                                |                                     Con                                     |
| :--------------------------------------------------------------: | :-------------------------------------------------------------------------: |
|                      Separated environments                      |                    Redundant duplication, waste of space                    |
|         Environment-specific configurations are possible         |               Performance can be slow, boot times can be long               |
| Environment configurations can be shared and reproduced reliably | Reproducing on another computer/ server is possible but may still be tricky |

|                     Docker Containers                      |                        Virtual Machines                         |
| :--------------------------------------------------------: | :-------------------------------------------------------------: |
|   Low impact on OS, very fast, minimal disk space usage    |      Bigger impact on OS, slower, higher disk space usage       |
|       Sharing, re-building and distribution is easy        |    Sharing, re-building and distribution can be challenging     |
| Encapsulate apps/ environments instead of "whole machines" | Encapsulate "whole machines" instead of just apps/ environments |

- <b>Docker Tools & Building blocks</b>:
  - Docker Engine
  - Docker Desktop (incl. Daemon & CLI)
  - Docker Hub
  - Docker Compose

&nbsp;

---

&nbsp;

- Foundation

  - Images & Containers
  - Data & Volumes (in Containers)
  - Containers & Networking

- "Real Life"
  - Multi-Container Projects
  - Using Docker-Compose
  - "Utility Containers"
  - Deploying Docker Containers
- Kubernetes
  - Basics
  - Data & Volumes
  - Networking
  - Deploying a Kubernetes Clusters

&nbsp;

---

&nbsp;

### Images & Containers

|                  Images                  |                      Containers                       |
| :--------------------------------------: | :---------------------------------------------------: |
|   Templates/ Blueprints for containers   |            The running "unit of software"             |
| Contains code + required tools/ runtimes | Multiple containers can be created based on one image |

- Using Pre-Built & Custom Images
  - [Docker Hub](https://hub.docker.com/)
  - A container is base on an image
- Creating & Managing Containers

![image-layers](./diagrams/image-layers.png)

&nbsp;

![image-containers](./diagrams/image-containers.png)

|                         Images                         |                      Containers                      |
| :----------------------------------------------------: | :--------------------------------------------------: |
| Can be <b>tagged</b> (named) <i>-t, docker tag ...</i> |          Can be <b>named</b> <i>--name</i>           |
|       Can be <b>listed</b> <i>docker images</i>        | Can be <b>configured in detail</b> see <i>--help</i> |
|   Can be <b>analyzed</b> <i>docker image inspect</i>   |        Can be <b>listed</b> <i>docker ps</i>         |
| Can be <b>removed</b> <i>docker rmi, docker prune</i>  |        Can be <b>removed</b> <i>docker rm</i>        |

- Image tags (name : tag)
  - <b>name: </b>Defines a <b>group</b> of, <b>possible more specialized</b>, images (e.g. "node")
  - <b>tag: </b>Defines a <b>specialized image within a group of images</b> (e.g. "14")
- Specify the version (tag) to use
- Docker Hub
  - Official Docker Image Registry
  - Pubic, private and "official" mages
- Private Registry
  - Any provider/registry you want to use
  - Only your own (or team) images <b>(Needs to be HOST:NAME to talk to private registry)</b>
  - Share: <code>docker push IMAGE_NAME</code>
  - Use: <code>docker pull IMAGE_NAME</code>

&nbsp;

---

&nbsp;

> <b>ahmet: </b>Pulling and running image
> Let's say I have pulled an image from Dockerhub which is a webserver listening a port, how can I know that which port it's listening without seeing code? Maybe we'll cover that in future lessons..
>
> <b>Maximilian: </b>That's why you typically should document that via EXPOSE in your Dockerfile. If you pull some image where you never saw the Dockerfile, it should be documented on Docker Hub.

&nbsp;

---

&nbsp;

### Data & Volumes

|                  Application                  |                 Temporary App Data                  |                    Permanent App Data                     |
| :-------------------------------------------: | :-------------------------------------------------: | :-------------------------------------------------------: |
|       Application (Code + Environment)        |    Temporary App Data (e.g. entered user input)     |            Permanent App Data (user accounts)             |
|  Written & provided by you (= the developer)  |       Fetched / Produced in running container       |          Fetched / Produced in running container          |
|  Added to image and container in build phase  |         Stored in memory or temporary files         |               Stored in files or a database               |
| “Fixed”: Can’t be changed once image is built |     Dynamic and changing, but cleared regularly     |      Must not be lost if container stops / restarts       |
|       Read-only, hence stored in Images       | Read + write, temporary, hence stored in Containers | Read + write, permanent, stored with Containers & Volumes |

- Volumes are folders on your host machine hard drive which are mounted (“made available”, mapped) into containers
  - Anonymous
  - Named
- Host (Your Computer) /some-path <---> /app/user-data
- Volumes persist if a container shuts down. If a container (re-)starts and mounts a volume, any data inside of that volume is available in the container.
- A container can write data into a volume and read data from it.
- <b>Bind Mounts </b>are great for persistent and editable data
- For Windows using WSL Tool, there is a need to access Linux filesystems

|                        Command                         |  Persist State   |
| :----------------------------------------------------: | :--------------: |
|        <code>docker run -v /app/data ...</code>        | Anonymous Volume |
|     <code>docker run -v data:/app/data ...</code>      |   Named Volume   |
| <code>docker run -v /path/to/code:/app/code ...</code> |    Bind Mount    |

|                       Anonymous Volumes                        |                         Named Volumes                          |                           Bind Mounts                            |
| :------------------------------------------------------------: | :------------------------------------------------------------: | :--------------------------------------------------------------: |
|          Created specifically for a single container           |    Created in general – not tied to any specific container     | Location on host file system, not tied to any specific container |
|   Survives container shutdown / restart unless --rm is used    | Survives container shutdown / restart – removal via Docker CLI |    Survives container shutdown / restart – removal on host fs    |
|              Can not be shared across containers               |                Can be shared across containers                 |                 Can be shared across containers                  |
| Since it’s anonymous, it can’t be re-used (even on same image) |      Can be re-used for same container (across restarts)       |       Can be re-used for same container (across restarts)        |

- <b>Read-only Volume</b>
- We remove <code>COPY . .</code> in the dockerfile while using bind mount run command but we will not be using it when we are in the production.

&nbsp;

---

&nbsp;

> <b>Lin: </b>Why do we not use bind mounts in production?

> <b>Adam: </b>You don't want to use bind mounts in production because they aren't very portable. If I gave you a command to start a container with an absolute path to the volume then you wouldn't be able to use it without editing it for your filesystem. Named volumes don't have that problem.

&nbsp;

---

&nbsp;

- Docker supports build-time <b>ARGuments</b> and runtime <b>ENVironment</b> variables

|                                      ARG                                      |                         ENV                          |
| :---------------------------------------------------------------------------: | :--------------------------------------------------: |
| Available inside of Dockerfile, NOT accessible in CMD or any application code | Available inside of Dockerfile & in application code |
|               Set on image build (docker build) via --build-arg               | Set via ENV in Dockerfile or via --env on docker run |

&nbsp;

---

&nbsp;
