<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li><a href="#commands">Commands</a></li>
    <li><a href="#basics">Basics</a></li>
    <li><a href="#images--containers">Images & Containers</a></li>
    <li><a href="#data--volumes">Data & Volumes</a></li>
    <li><a href="#networking">Networking</a></li>
    <li><a href="#multi-containers-app">Multi-Containers App</a></li>
  </ol>
</details>

&nbsp;

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

## Images & Containers

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
  - Share: `docker push IMAGE_NAME`
  - Use: `docker pull IMAGE_NAME`

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

## Data & Volumes

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

|                      Command                      | Persist State |
| :-----------------------------------------------: | :-----------: |
|        `docker run -v /app/data ...</code>        | Anonymous V`  |
|     `docker run -v data:/app/data ...</code>      |  Named Vol`   |
| `docker run -v /path/to/code:/app/code ...</code> |   Bind Mou`   |

|                       Anonymous Volumes                        |                         Named Volumes                          |                           Bind Mounts                            |
| :------------------------------------------------------------: | :------------------------------------------------------------: | :--------------------------------------------------------------: |
|          Created specifically for a single container           |    Created in general – not tied to any specific container     | Location on host file system, not tied to any specific container |
|   Survives container shutdown / restart unless --rm is used    | Survives container shutdown / restart – removal via Docker CLI |    Survives container shutdown / restart – removal on host fs    |
|              Can not be shared across containers               |                Can be shared across containers                 |                 Can be shared across containers                  |
| Since it’s anonymous, it can’t be re-used (even on same image) |      Can be re-used for same container (across restarts)       |       Can be re-used for same container (across restarts)        |

- <b>Read-only Volume</b>
- We remove `COPY . .</code> in the dockerfile while using bind mount run command but we will not be using it when we are in the prod`

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

> <b>Environment variables and security: </b>Depending on which kind of data you're storing in your environment variables, you might not want to include the secure data directly in your Dockerfile.
>
> Instead, go for a separate environment variables file which is then only used at runtime (i.e. when you run your container with docker run). Otherwise, the values are "baked into the image" and everyone can read these values via `docker history IMAGE<`
>
> For some values, this might not matter but for credentials, private keys etc. you definitely want to avoid that! If you use a separate file, the values are not part of the image since you point at that file when you run docker run. But make sure you don't commit that separate file as part of your source control repository, if you're using source control.

&nbsp;

---

&nbsp;

## Networking

- Container to WWW communication
- Container to local host machine
- Container to container communication

![containers-and-network-requests](./diagrams/containers-and-network-requests.png)

&nbsp;

![docker-ip-resolving](./diagrams/docker-ip-resolving.png)

> Docker Networks actually support different kinds of <b>"Drivers"</b> which influence the behavior of the Network. The default driver is the <b>"bridge" driver</b> - it provides the behavior shown in this module (i.e. Containers can find each other by name if they are in the same Network).
>
> The driver can be set when a Network is created, simply by adding the `--driver</code> `
>
> `docker network create --driver bridge my-net`
>
> Of course, if you want to use the "bridge" driver, you can simply omit the entire option since "bridge" is the default anyways. Docker also supports these alternative drivers - though you will use the "bridge" driver in most cases:
>
> <b>host: </b>For standalone containers, isolation between container and host system is removed (i.e. they share localhost as a network)
>
> <b>overlay: </b>Multiple Docker daemons (i.e. Docker running on different machines) are able to connect with each other. Only works in "Swarm" mode which is a dated / almost > deprecated way of connecting multiple containers
>
> <b>macvlan: </b>You can set a custom MAC address to a container - this address can then be used for communication with that container
>
> <b>none: </b>All networking is disabled.
>
> <b>Third-party plugins: </b>You can install third-party plugins which then may add all kinds of behaviors and functionalities
>
> As mentioned, the "bridge" driver makes most sense in the vast majority of scenarios.

&nbsp;

---

&nbsp;

> <b>John: </b>Swarm, outdated or out branded?
>
> You cited Swarm as "dated / almost deprecated way of connecting multiple containers". Interesting as Bret Fisher, Docker Captain who does most of Docker's release cycle updates for the community has a very different take. He prefers Swarm but realizes Kubes has overwhelmed the community with marketing.
>
> Secondary, Swarm is less complicated though Kubes is trying to uncomplicate itself. Kubes also has higher system requirements. If you have massive complexity and scale extrodinaire then yes, Kubes is a winning choice. It has been said the first rule of architecture is "Everything in software architecture is a tradeoff". Kubes is no exception, and Swarm is also no exception. Swarm is the best choice in many situations.
>
> P.S. When I got my Docker Enterprise course certificate, official training, the instructor just two years ago said that eight out of ten deployments were on Swarm. Also, Mirantis was going to do away with Swarm and due to customer input have pulled Swarm back into long term support plans. Remember, K.I.S.S.? Why do Kubes if it's not needed?
>
> <b>Maximilian: </b>Yeah, swarm can be easier to get started with - still, I'm not convinced by Swarm's future.
>
> You will find different opinions out there for sure but whilst Kubernetes is clearly under very active development, the same can't really be said for Swarm. You can use it and it might "not go anywhere" but it also doesn't look like it's really being embraced by large chunks of the community.
>
> This [article](https://medium.com/@markuman/is-docker-swarm-mode-eol-7a3f316116a3) is also quite interesting.
>
> Feel free to use whatever you personally prefer - Docker Swarm might do the trick of course. But I definitely see Kubernetes being and becoming more important.

&nbsp;

---

&nbsp;

## Multi-Containers App

- [Docker Hub Mongo image - Authentication](https://hub.docker.com/_/mongo/)

### goals-app

> <b>Bernard: </b>Better solution for the goals app
> A better solution is to use the proxy feature of create-react-app (based on webpack dev server). Add the following line to your frontend package.json:
>
> `"proxy": "http://goals-backend:80"`
>
> Then, you can stop mapping the port 80 from the backend. Modify the react App.js to connect to `localhost:3000` instead of `localhost`.
>
> In this setup, only the frontend app (port 3000) is exposed and all backend calls are proxied inside the container network. This is solution is more secure and ressemble better a setup which could be used in production.

&nbsp;

---

&nbsp;
