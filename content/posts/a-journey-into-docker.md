---
date: "2020-12-19T01:29:14+06:00"
title: "A Journey into the Docker World"
---

---

## What is Docker?
Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package — [OpenSource.com, What is Docker?](https://opensource.com/resources/what-docker)

Docker enables us to separate our applications from our infrastructure. So we developers can focus on writing code without worrying about the system it will ultimately run on.

---

## Concepts

Here is a very brief summary of the key terms we need to be familiar with when working with Docker.

#### Dockerfile :
A Dockerfile is a blueprint for building Docker images. It is simply a text file that contains the build instructions to build a a Docker image.

#### Image : 
Docker images are executable packages that include everything needed to run an application — the code, a runtime, libraries, environment variables, and configuration files. An image is a read-only template with instructions for creating a Docker container. We can build our own images (using a Dockerfile) or use images that have been built by others and are available in a registry (such as Docker Hub).

#### Container : 
A Docker container is a running instance of a Docker image. A container is an isolated environment which can expose ports and volumes to interact with other containers or/and the outer world.

#### Volume : 
Volumes are the “data” part of a container. They are designed to persist data and share between containers. Volumes are independent of the container’s lifecycle.

#### Docker Compose : 
Docker Compose is a tool for defining and running multi-container Docker applications. The `docker-compose.yml` file allows us to configure all our application's services in one place and start them all with a single command.

#### Docker Hub :
A Docker registry stores Docker images. [Docker Hub](https://hub.docker.com/) is the default public registry which is managed by Docker (the company). We can find images for most of the apps and linux distros we need there. Anybody can build and host their Docker images on Docker Hub. It's like github for Docker images.

---

## Architecture

Everything starts with the Dockerfile. It is the source code of the Image. Once the Dockerfile is created, we build the image using that file. Next, we can use the image to run containers. A running container is an isolated environment. We can create, start, stop, move, or delete a container using the Docker API or CLI. We can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

![Architectire](https://docs.docker.com/engine/images/architecture.svg)

*image source: [docker docs](https://docs.docker.com/get-started/overview/#docker-architecture)*

---

## Docker Commands : Cheat Sheet

**-** download images (from docker hub) to our computer
```bash
$ docker pull <image>
```

\
**-** build an image from a Dockerfile
```bash
$ docker build <path>

# example : build a image (using the Dockerfile in the current directory) with a tag named my-image
$ docker build --tag my-image .

# By default the docker build command will look for a Dockerfile at the root of the build context.
# We can specify an alternative file using the -f (or --file) option. for example, the command below
# will build a image from the Dockerfile.dev file 
$ docker build -f Dockerfile.dev .
```

\
**-** list of images (that have been downloaded/built)
```bash
$ docker images
```

\
**-** remove images
```bash
$ docker rmi <image1> <image2>
````

\
**-** run a container
```bash
$ docker run <image>
# note : docker run = docker create + docker start + docker attach
```

```bash
# example : docker run with options  :
# --------------------------------------
# Run a container 
# - from the specific image,
# - name the running container “my_container”,
# - expose port 5000 externally and
# - mapped to port 80 inside the container
$ docker container run --name my_container -p 5000:80 <image>
````

\
**-** list of containers

```bash
$ docker ps      # list out the running containers only
$ docker ps -a   # list out all contaiers (including  the stopped containers)
````

\
**-** executing commands inside a running container
```bash
$ docker exec <container> <command>

# example : enter the bash of a container
$ docker exec -it <container> bash
````

\
**-** accessing logs from a running container
```bash
$ docker logs <container>

# get logs realtime
$ docker logs -f <container>
````

\
**-** stop/kill containers
```bash
$ docker stop <container> # stop gracefully
$ docker kill <container> # stop immediately
````

\
**-** remove one or more containers
```bash
$ docker rm <container>
````

\
**-** remove unused data
```bash
$ docker system prune
````


Few Notes:
- `docker start` runs any container that is not already running. 
- `docker restart` kills the running container and starts that again.
- `docker run` creates and starts a new container every time.

> *Assume a scenario, where we're working inside a container for a while. Then we stop the container and on the next day we run the container once again using `docker run` command. We'll see that all of our works have been lost. So we should remember to start previously created containers using the `docker start` command and not the `docker run` command.*

---

## Dockerfile

Every single Docker container begins as a pure vanilla Linux machine that knows nothing. We need to tell the container everything it needs to know — all the dependencies it needs to download and install in order to run the application. We do that with a [Dockerfile](https://docs.docker.com/engine/reference/builder/).

A Dockerfile is simply a text file that contains the build instructions to build a a Docker image. It contains all the commands a user could call on the command line to assemble an image.

### Example : 
Let's start with a very simple example by creating a Dockerfile to run an ubuntu container. 

**-** Create a new file named *Dockerfile* and put the following instructions there:

```dockerfile
# Get the base ubuntu 18.04 from Docker hub
FROM ubuntu:18.04

# Command to execute when we run the container
CMD echo "Hello World!"
```

\
**-** Let's build an image from that Dockerfile. Note that, we need to run the command from the same directory where we have our Dockerfile.
```bash
$ docker build .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM ubuntu:18.04
 ---> 56def654ec22
Step 2/2 : CMD echo "Hello World!"
 ---> Running in a49ebaf5c0f1
Removing intermediate container a49ebaf5c0f1
 ---> 339710e878e8
Successfully built 339710e878e8
```
We can see that the Docker image was successfully built and the ID of the image is **339710e878e8**. 

\
**-** Let's now start and run a container from that image.

```bash
$ docker run 339710e878e8
Hello World!
```

Great! So now we have an Ubuntu container running inside our machine. We can enter into the shell of that container, install new packages, and run commands in the same way as we would do on any other Ubuntu machine.


### Common Dockerfile Instructions :

Docker can build images automatically by reading the instructions from a Dockerfile. In this list below I have included some of the most frequently used Dockerfile Instructions. For the complete list, please go through the [documentation](https://docs.docker.com/engine/reference/builder/).

**FROM** — Sets the base image for subsequent instructions. A Dockerfile must start with a FROM instruction.

**RUN** — Execute commands in a new layer on top of the current image and commit the results.

**CMD** - Sets a default command, which will be executed when we run the container.

**ENTRYPOINT** - Specifies a command that will always be executed when the container starts (unless we add the `--entrypoint` flag).

> *Note: The RUN, CMD, and ENTRYPOINT instructions are used to run commands. These instructions look similar and cause confusion among developers. We should know the difference between [CMD, RUN, and ENTRYPOINT](https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/).*

**ENV** — Sets the environment variable.

**COPY**- Copies new files or directories (from host) into the filesystem of the container.

**ADD** - Copies new files, directories, or remote file URLs. We can also extract a tar file from the source directly into the destination.

> *Note: It's best practice to use COPY. We should avoid the ADD command unless we need to extract a local tar file.*

**VOLUME** — Creates a mount point with the specified name and marks it as holding externally mounted volumes from the native host or other containers.

**EXPOSE** — Informs Docker that the container listens on the specified network ports at runtime.
> *Note: Most people confuse exposing a port with publishing a port. This [stackoverflow answer](https://stackoverflow.com/a/47594352/3158021) explained the difference very well. 
> The EXPOSE instruction does not actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container, about which ports are intended to be published. To actually publish the port when running the container, use the `-p` flag on docker run to publish and map one or more ports, or the `-P` flag to publish all exposed ports and map them to high-order ports - [documentation](https://docs.docker.com/engine/reference/builder/#expose).*

---

## Docker Compose

[Docker Compose](https://docs.docker.com/compose/) is a tool for defining and running multi-container Docker applications. With Docker Compose, we use a YAML file to configure our application’s services. Then, we create and start all the services from that configuration with a single command.

Imagine, we have a simple web application which is composed of 3 different services: client(React App), server(Django API Backend) and database(PostgreSQL). We can use docker compose to run the entire application with a single command.

#### Difference between Docker and Docker-Compose :
Docker is used to manage an individual container (service) for our application. Docker-Compose is used to manage multiple container applications.

![docker-vs-docker-compose](https://miro.medium.com/max/700/1*LHq5mhynSjYBIhfgY3czkQ.png)

*image source: [freeCodeCamp](https://medium.com/free-code-camp/a-beginners-guide-to-docker-how-to-create-a-client-server-side-with-docker-compose-12c8cf0ae0aa)*

### Compose File :
The Compose file is a [YAML](https://yaml.org/) file defining services, networks, and volumes for a Docker application. There are [several versions](https://docs.docker.com/compose/compose-file/compose-versioning/) of the docker-compose file.

### Steps :

Using Compose is basically a three-step process:

1. Define your app’s environment with a Dockerfile.
2. Define the services that make up your app in compose file (*docker-compose.yml*) so that thy can be run together in an isolated environment.
3. Run command (`docker-compose up`) to start and run the entire app.

To get started with Docker Compose, please follow the [official documentation](https://docs.docker.com/compose/gettingstarted/).

---

## References

##### Docker:
- [Docker Docs](https://docs.docker.com/)
- [freeCodeCamp : The Docker Handbook](https://www.freecodecamp.org/news/the-docker-handbook)
- [towardsdatascience : Why you should care about Docker?](https://towardsdatascience.com/why-you-should-care-about-docker-9622725a5cb8)
- [Red Hat Developers : docker CLI & Dockerfile Cheat Sheet](https://design.jboss.org/redhatdeveloper/marketing/docker_cheatsheet/cheatsheet/images/docker_cheatsheet_r3v2.pdf)

##### Docker Compose:
- [Docker Docs](https://docs.docker.com/compose/)
- [medium : Using Docker Compose to Run Your Applications](https://medium.com/rate-engineering/using-docker-containers-to-run-a-distributed-application-locally-eeabd360bca3)
- [medium : A beginner’s guide to Docker — how to create a client/server side with Docker-Compos](https://medium.com/free-code-camp/a-beginners-guide-to-docker-how-to-create-a-client-server-side-with-docker-compose-12c8cf0ae0aa)

