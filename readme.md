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

> Docker is an open platform for Developing, Packaging, Shipping and Running applications.

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

 - Linux [x86-64](https://www.wikiwand.com/en/X86-64) & Windows (Server 2016+)
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

Creates servers, installs Docker on them and configures the Docker client to talk to them.

![Docker machine logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_machine.png)

---

### Docker compose

A tool for defining and running complex applications with Docker
(eg a multi-container application) with a single file.

![Docker compose logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_compose.png)

---

### Docker swarm

Swarm pools together several Docker hosts and exposes them as a single virtual Docker host (clustering).
It scales up to multiple hosts.

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

### Docker examples

- SSH into a container
- Build an image
- Docker [Volume](https://docs.docker.com/engine/userguide/containers/dockervolumes/)
- Common Docker Commands
- [Linked](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/) containers
- Using [docker-compose](https://docs.docker.com/compose/)
- Scale with docker-compose
- Screen and sound within containers

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

### Example: Common Docker Commands

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
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER]
docker rm [CONTAINER]

```
Screencast: [Common Docker commands](https://asciinema.org/a/3hczjxzuvih674htyis6o8q6t)

---

### Example: Docker link containers

Let's create a [JBoss Ticket Monster app](https://github.com/jboss-developer/ticket-monster)

```
docker pull rafabene/wildfly-ticketmonster
docker pull postgres:9.4
docker pull donnex/pgweb

// Start a container for postgres
docker run -d --name postgres_db \
           -e POSTGRES_USER=ticketmonster \
           -e POSTGRES_PASSWORD=ticketmonster-docker \
           postgres:9.4

// Create a container for Ticket Monster app
// Usage: --link [name or id]:alias
docker run -d --name ticketmonster \
           -p 8088:8080 \
           --link postgres_db:db \
           rafabene/wildfly-ticketmonster-h2

// Open http://localhost:8088/ticket-monster/ to see the App UI

// There is a proper linking
docker inspect -f "{{ .HostConfig.Links }}" ticketmonster

// Link a pgweb ui
docker run -d -p 8022:8080 \
           --link postgres_db \
           donnex/pgweb

// Open http://localhost:8022 and connect to the Pgweb UI
// Tip to find the Postgres credentials.
// Type: docker inspect --format='{{json .Config}}' postgres_db

```

---

### Example: Using Docker Compose

Let's do the same but with [docker-compose.yml](https://github.com/theodorosploumis/docker-java/blob/master/examples/docker-compose/docker-compose.yml)

```
git clone git@github.com:theodorosploumis/docker-java.git ~/docker-java
cd ~/docker-java/examples/docker-compose

// Run docker-compose using the docker-compose.yml
docker-compose up -d

// Same as previous
// Eg open http://localhost:8088/ticket-monster/ etc
```

---

### Example: Scale with Docker Compose

Following from previous...

```
// Create up to 10 Ticket Monster apps
docker-compose scale mywildfly=10

// Get their IP addresses
docker ps

// Open several apps (eg http://localhost:32781 etc)
// All apps share the same database
```

---

### Example: GUI with Docker

See examples at [hub.docker.com/u/jess](https://hub.docker.com/u/jess/)

```
// Grant access to everyone on the X Server (locally)
// Otherwise the containers below will never start
xhost +

// Libreoffice
docker run -it \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -e DISPLAY=unix$DISPLAY \
           --name cathode \
           jess/cathode

// SublimeText 3
docker run -it \
           -e NEWUSER=$USER \
           -v $HOME/.config/sublime-text-3/:/root/.config/sublime-text-3 \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -e "DISPLAY=unix${DISPLAY}" \
           --name sublime_text \
           jess/sublime-text-3

// Audacity (sound in docker container)
docker run --rm \
            -u $(id -u):$(id -g) \
            -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
            -v /dev/snd:/dev/snd \
            -v "$HOME:$HOME" \
            -w "$HOME" \
            -e DISPLAY="unix$DISPLAY" \
            -e HOME \
            $(find /dev/snd/ -type c | sed 's/^/--device /') \
            knickers/audacity

// Disable access to x11
xhost -

```

---

### Docker tips

There are known best practices (see a list at [examples/tips](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/tips))

- Optimize containers (see [imagelayers.io](https://imagelayers.io/?images=maven:3.3.1-jdk-8))
- Create your own, tiny base images
- Containers are not Virtual Machines
- Full stack Images VS 1 process per Container
- Use files/scripts to setup container
- Prefer using docker-compose
- Production needs orchestration tools

---

### The Docker war

| Type | Software |
|----|----------|
| Cluster & <br>orchestrate | [Swarm](https://docs.docker.com/swarm/), [Kubernetes](http://kubernetes.io/), [Marathon](https://mesosphere.github.io/marathon/), [MaestroNG](https://github.com/signalfx/maestro-ng), [decking](http://decking.io/), [shipyard](http://shipyard-project.com/) |
| Registry | [Portus](http://port.us.org/), [Docker Distribution](https://github.com/docker/distribution), [Docker Hub](http://hub.docker.com), [Quay](https://quay.io), [Google Container Reg.](https://cloud.google.com/tools/container-registry/), [Artifactory](https://www.jfrog.com/artifactory/), [ProjectAtomic](http://www.projectatomic.io/), [Treescale](https://treescale.com/), [Canister](https://www.canister.io/) |
| PaaS | [Rancher](http://rancher.com/), [Tsuru](https://tsuru.io/), [dokku](https://github.com/dokku/dokku), [flynn](https://flynn.io/),  [Octohost](http://octohost.io/), [DEIS](http://deis.io/) |

---

### Docker Alternatives

- [Rocket, rkt](https://github.com/coreos/rkt)
- [Linux Containers, LXC](https://linuxcontainers.org/)
- [OpenVZ](https://openvz.org/)
- [BSD Jails](https://www.freebsd.org/doc/handbook/jails.html)
- [Solaris Zones](http://oracle.com/solaris)
- [drawbridge](http://research.microsoft.com/en-us/projects/drawbridge/)

---

### Instead of Resources

 - [Awesome Docker](https://github.com/veggiemonk/awesome-docker) (list of Docker resources & projects)
 - [Docker cheat sheet](https://github.com/wsargent/docker-cheat-sheet)
 - [Docker in Practice](https://www.manning.com/books/docker-in-practice), [The Docker Book](http://www.dockerbook.com/), [Docker for Java Developers - free](http://shop.oreilly.com/product/0636920050872.do) (books)
 - [Docker aliases/shortcuts](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/shortcuts/docker-aliases.sh)
 - Docker [case studies](https://www.docker.com/customers)

---

### Questions?

[Review this presentation](https://goo.gl/w1ZmXo)

> Next: Docker in production, Scaling, Private registries, PaaS.

###### Tools used: [oh my zsh](http://ohmyz.sh/) / [reveal.js](https://github.com/hakimel/reveal.js) / [Simple Docker UI for Chrome](https://github.com/felixgborrego/docker-ui-chrome-app) / [docker compose 1.9.0](https://github.com/docker/compose/releases/tag/1.9.0) / [docker 1.12.3](https://github.com/docker/docker/releases/tag/v1.12.3)
