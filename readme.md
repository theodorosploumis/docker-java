![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_logo.png)

## Docker with Java - Introduction

#### [Java Meetup Thessaloniki](http://meetu.ps/33dmsB), 2016

###### [TheodorosPloumis.com](http://www.theodorosploumis.com/en) / [@theoploumis](http://twitter.com/theoploumis)
________________________

###### Get them: [online presentation](http://theodorosploumis.github.io/docker-java/) / [source code](https://github.com/theodorosploumis/docker-java) / [docker image](https://hub.docker.com/r/tplcom/docker-java/)

###### Under [Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/) license.

---

### Let me ask you

- Who knows about [Docker](https://www.docker.com/)?
- Who uses Docker for development?
- Who uses Docker in production?
- Who tried but could not do it?

---

### What is Docker (v1.12.3)

> Docker is an open platform for Developing, Shipping and Running applications.

OR

> Docker allows you to Package an application with all of its Dependencies into a standardized unit for software development.

---

### Docker vs VMs

![Docker vs traditional Virtualization](https://insights.sei.cmu.edu/assets/content/VM-Diagram.png)

---

### Docker History

 - Solomon Hykes ([@solomonstre](https://twitter.com/solomonstre))
 - dotCloud (now Docker Inc)
 - March 2013
 - Apache 2.0 license
 - 37k stars on [Github](https://github.com/docker/docker)
 - 270k public repositories on docker hub

---

### Docker Benefits

 - Fast (deployment, migration, restarts)
 - Secure
 - Lightweight (save disk & CPU)
 - Open Source
 - Portable software
 - Microservices and integrations (APIs)
 - Simplify DevOps
 - Version control capabilities

---

### Common Docker usages

 - Scaling apps
 - Development collaboration
 - Infrastructure configuration
 - Sandbox (develop, test, debug, educate etc)
 - Local development
 - Continuous Integration & Deployment
 - Multi-tier applications
 - PaaS, SaaS

###### See the [survey results for 2016](https://www.docker.com/survey-2016)

---

### Technology stack

 - Linux [x86-64](https://www.wikiwand.com/en/X86-64) & Windows (Hyper-V)
 - [Go](https://golang.org/) language
 - [Client - Server](https://www.wikiwand.com/en/Client%E2%80%93server_model) (deamon) architecture
 - Union file systems ([UnionFS](https://www.wikiwand.com/en/UnionFS): AUFS, btrfs, vfs etc)
 - [Namespaces](https://en.wikipedia.org/wiki/Cgroups#NAMESPACE-ISOLATION) (pid, net, ipc, mnt, uts)
 - Control Groups ([cgroups](https://www.wikiwand.com/en/Cgroups))
 - Container format ([libcontainer](https://github.com/opencontainers/runc/tree/master/libcontainer "Libcontainer provides a native Go implementation for creating containers with namespaces, cgroups, capabilities, and filesystem access controls. It allows you to manage the lifecycle of the container performing additional operations after the container is created."))

###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### The Docker architecture

![Docker architecture](https://docs.docker.com/engine/article-img/architecture.svg)
###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### Docker components

 - (Docker) client
 - daemon
 - engine
 - machine
 - compose
 - swarm
 - registry

---

### Docker client

It is the primary user interface to Docker. It accepts commands from the user
and communicates back and forth with a Docker daemon.

---

### Docker daemon

It runs on a host machine. The user does not directly interact with the daemon,
but instead through the Docker client with the RESTful api or sockets.

---

### Docker engine

A Client with a Daemon as also as the docker-compose tool. Usually referred simply as "docker".

![Docker engine logo](https://raw.githubusercontent.com/theodorosploumis/docker-java/master/img/docker_logo_simple.png)

---

### Docker machine

A tool which makes it really easy to create Docker hosts on your computer,
on cloud providers and inside your own data center.
It creates servers, installs Docker on them, then configures the Docker client to talk to them.

![Docker machine logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_machine.png)

---

### Docker compose

A tool for defining and running complex applications with Docker
(eg a multi-container application) with a single file.

![Docker compose logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_compose.png)

---

### Docker swarm

A native clustering tool for Docker. Swarm pools together several Docker
hosts and exposes them as a single virtual Docker host. It scale up to multiple hosts.

![Docker swarm logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_swarm.png)

---

### Docker distribution

A (hosted) service containing repositories of images which responds to the Registry API.

![Docker distribution logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_distribution.png)

---

### The Docker Components diagram

![Docker components](https://raw.githubusercontent.com/theodorosploumis/docker-java/master/img/docker-components.png)

---

### Steps of a Docker workflow

```
docker run -i -t ubuntu:15.04 /bin/bash
```

 - Pulls the ubuntu:15.04 [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
 - Creates a new [container](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
 - Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
 - Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29)
 - Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication.")
 - Executes a process that you specify (``` /bin/bash ```)
 - Captures and provides application output

Screencast: [Steps of a Docker workflow](https://asciinema.org/a/1yqyy1uu1taxciqf4136sy3ld).

---

### The docker image

![ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/image-layers.jpg "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot. Each Docker image references a list of read-only layers that represent filesystem differences. Layers are stacked on top of each other to form a base for a container’s root filesystem.")

---

### The docker container

![container using ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/container-layers.jpg "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides. For each containers there is a new, thin, writable layer - container layer - on top of the underlying stack (image).")

---

### The Dockerfile

> A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

 - [Dockerfile with inline comments](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/dockerfile/Dockerfile) just for education
 - [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) on docker docs
 - Public Dockerfiles ([wildfy](https://github.com/jboss-dockerfiles/wildfly/blob/master/Dockerfile), [Spring Boot](https://github.com/Bankmonitor/docker/blob/master/Dockerfile), [openjdk 9](https://github.com/docker-library/openjdk/blob/master/9-jre/Dockerfile))

---

### Common Docker Commands

```
// General info
man docker // man docker run
docker help // docker help run
docker info
docker version
docker network ls

// Images
docker images // docker [IMAGE_NAME]
docker pull [IMAGE] // docker push [IMAGE]

// Containers
docker run
docker ps // docker ps -a, docker ps -l
docker stop/start/restart [CONTAINER]
docker stats [CONTAINER]
docker top [CONTAINER]
docker port [CONTAINER]
docker inspect [CONTAINER]
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER]
docker rm [CONTAINER]

```
Screencast: [Common Docker commands](https://asciinema.org/a/3hczjxzuvih674htyis6o8q6t)

---

### Docker examples

- SSH into a container
- Build an image
- Docker [Volume](https://docs.docker.com/engine/userguide/containers/dockervolumes/)
- [Linked](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/) containers
- Using [docker-compose](https://docs.docker.com/compose/)
- Scale containers with docker-compose
- Share an image (share this presentation)
- Package an app with its environment
- Screen and sound within containers (x-forward)

---

### Example: SSH into a container

```
docker pull ubuntu
docker run -it --name ubuntu_example ubuntu /bin/bash
```
Screencast: [SSH into a container](https://asciinema.org/a/0z4bu6ub4l3z6n3t6b0d5e35g)

---

### Example: Build an Image

Let's build a [jenkins image](https://github.com/komljen/dockerfile-examples/blob/master/jenkins/Dockerfile)

```
git clone git@github.com:komljen/dockerfile-examples.git ~/Docker-presentation
cd ~/Docker-presentation/jenkins
docker build -t jenkins-local .

// Test it
docker run -d -p 8099:8080 --name jenkins_example jenkins-local

// Open http://localhost:8099
curl localhost:8099
```
Screencast: [Docker build an image](https://asciinema.org/a/36gcw7ssyat360t59nfn6ete5)

---

### Example: Docker volume

Let's use [Apache server](https://bitbucket.org/EdBoraas/apache-docker/src/)

```
cd ~/Docker-presentation
mkdir apache-example
cd apache-example

docker pull eboraas/apache
docker run --name apache_volume_example \
           -p 8180:80 -p 443:443 \
           -v $(pwd):/var/www/ \
           -d eboraas/apache

// Locally create an index.html file
mkdir html
cd html
echo "It works using docker volume." >> index.html

// Open http://localhost:8180 to view the html file
curl localhost:8180
```
Screencast: [Docker simple volume example](https://asciinema.org/a/ep1ugo3eokl2nkjap054cgmqj)

---

### Example: Docker link containers

Let's create a [Drupal app](https://hub.docker.com/_/drupal/) (apache, php, mysql, drupal)

```
cd ~/Docker-presentation
mkdir drupal-link-example
cd drupal-link-example

docker pull drupal:8.2.3-apache
docker pull mysql:8

// Start a container for mysql
docker run --name mysql_example \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=drupal \
           -e MYSQL_USER=drupal \
           -e MYSQL_PASSWORD=drupal \
           -d mysql:5.5

// Start a Drupal container and link it with mysql
// Usage: --link [name or id]:alias
docker run -d --name drupal_example \
           -p 8280:80 \
           --link mysql_example:mysql \
           drupal:8.2.3-apache

// Open http://localhost:8280 to continue with the installation
// On the UI for the db host use: mysql

// There is a proper linking
docker inspect -f "{{ .HostConfig.Links }}" drupal_example
```

---

### Example: Using Docker Compose

Let's create a Drupal app with [docker-compose.yml](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/docker-compose/docker-compose.yml)

```
cd ~/Docker-presentation
git clone git@github.com:theodorosploumis/docker-presentation.git
cd docker-presentation/examples/docker-compose

// Run docker-compose using the docker-compose.yml
cat docker-compose.yml
docker-compose up -d
```

---

### Example: Share a public Image

```
cd ~/Docker-presentation
git clone git@github.com:theodorosploumis/docker-presentation.git
cd docker-presentation

docker pull nimmis/alpine-apache
docker build -t tplcom/docker-presentation .

// Test it
docker run -itd --name docker_presentation \
           -p 8480:80 \
           tplcom/docker-presentation

// Open http://localhost:8480, you should see this presentation

// Push it on the hub.docker.com
docker push tplcom/docker-presentation
```

---

### Example: Export/Save/Load etc

```
docker pull nimmis/alpine-apache
docker run -d --name apache_example \
           nimmis/alpine-apache

// Create a file inside the container.
// See https://github.com/nimmis/docker-alpine-apache for details.
docker exec -ti apache_example \
            /bin/sh -c 'mkdir /test && echo "This is it." >> /test/test.txt'

// Test it. You should see message: "This is it."
docker exec apache_example cat /test/test.txt

// Commit the change.
docker commit apache_export_example myapache:latest

// Create a new container with the new image.
docker run -d --name myapache_example myapache

// You should see the new folder/file inside the myapache_example container.
docker exec myapache_example cat /test/test.txt

// Export the container as image
cd ~/Docker-presentation
docker export myapache_example > myapache_example.tar

// Import a new image from the exported files
cd ~/Docker-presentation
docker import myapache_example.tar myapache:new

// Save a new image as tar
docker save -o ~/Docker-presentation/myapache_image.tar myapache:new

// Load an image from tar file
docker load < myapache_image.tar

```

---

### Example: GUI with Docker

See examples at [hub.docker.com/u/jess](https://hub.docker.com/u/jess/)

```
// Before staring we should grant access to everyone on the X Server (locally)
// Otherwise the containers below will never start and they will not be able to use x11
xhost +

// Libreoffice
docker run  -d \
            -v /etc/localtime:/etc/localtime:ro \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -e DISPLAY=unix$DISPLAY \
            -e GDK_SCALE \
            -e GDK_DPI_SCALE \
            --name libreoffice \
            jess/libreoffice

// SublimeText 3
docker run -it \
           -v $HOME/.config/sublime-text-3/:/root/.config/sublime-text-3 \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -e DISPLAY=$DISPLAY \
           --name sublime_text \
           jess/sublime-text-3

// Audacity (sound in docker container)
docker run  -d \
            -v /etc/localtime:/etc/localtime:ro \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -e DISPLAY=unix$DISPLAY \
            -e QT_DEVICE_PIXEL_RATIO \
            --device /dev/snd \
            --group-add audio \
            --name audacity \
            jess/audacity

// Disable access to x11
xhost -

```

---

### Docker tips

There are known best practices (see a list at [examples/tips](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/tips))

- Optimize containers (check [fromlatest.io](https://www.fromlatest.io/) and [imagelayers.io](https://imagelayers.io))
- Create your own tiny base
- Containers are not Virtual Machines
- Full stack Images VS 1 process per Container
- Create your private registry
- Create shortcut commands
- Use docker-compose.yml templates (see why at [lorry.io](https://lorry.io/))
- Be aware of the hub.docker.com docker agent version

---

### The Docker war

| Type | Software |
|:----:|----------|
| Clustering/orchestration | [Swarm](https://docs.docker.com/swarm/), [Kubernetes](http://kubernetes.io/), [Marathon](https://mesosphere.github.io/marathon/), [MaestroNG](https://github.com/signalfx/maestro-ng), [decking](http://decking.io/), [shipyard](http://shipyard-project.com/) |
| Docker registries | [Portus](http://port.us.org/), [Docker Distribution](https://github.com/docker/distribution), [hub.docker.com](http://hub.docker.com), [quay.io](https://quay.io), [Google container registry](https://cloud.google.com/tools/container-registry/), [Artifactory](https://www.jfrog.com/artifactory/), [projectatomic.io](http://www.projectatomic.io/), [Treescale.com/](https://treescale.com/), [Canister.io/](https://www.canister.io/) |
| PaaS with Docker | [Rancher](http://rancher.com/), [Tsuru](https://tsuru.io/), [dokku](https://github.com/dokku/dokku), [flynn](https://flynn.io/),  [Octohost](http://octohost.io/), [DEIS](http://deis.io/) |
| OS made of Containers | [RancherOS](http://rancher.com/rancher-os/) |

---

### Docker Alternatives

- [Rocket, rkt](https://github.com/coreos/rkt)
- [Linux Containers, LXC](https://linuxcontainers.org/)
- [Linux container hypervisor, LXD](http://www.ubuntu.com/cloud/lxd)
- [BSD Jails](https://www.freebsd.org/doc/handbook/jails.html)
- [Solaris Zones](http://oracle.com/solaris)
- [drawbridge](http://research.microsoft.com/en-us/projects/drawbridge/)

---

### Instead of Resources

 - [Awesome Docker](https://github.com/veggiemonk/awesome-docker) (list of Docker resources & projects)
 - [Docker cheat sheet](https://github.com/wsargent/docker-cheat-sheet)
 - [Docker in Practice](https://www.manning.com/books/docker-in-practice), [The Docker Book](http://www.dockerbook.com/) (books)
 - [Docker aliases/shortcuts](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/shortcuts/docker-aliases.sh)
 - Docker [case studies](https://www.docker.com/customers)

---

### Questions?

[Review this presentation](#)

> Next: Docker in production, Scaling, Private registries, PaaS.

###### In this presentation I have used: [oh my zsh](http://ohmyz.sh/) / [reveal.js](https://github.com/hakimel/reveal.js) / [Simple Docker UI for Chrome](https://github.com/felixgborrego/docker-ui-chrome-app) / [docker compose 1.9.0](https://github.com/docker/compose/releases/tag/1.9.0) / [docker 1.12.3](https://github.com/docker/docker/releases/tag/v1.12.3)
