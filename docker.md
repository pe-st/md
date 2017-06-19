docker
======

## Meta

Note: if you are using a remote Docker daemon, such as Boot2Docker, then do not type the sudo before the docker commands shown in the documentation's examples.

Artifactory has docker extension


## Docker Architecture

https://docs.docker.com/engine/understanding-docker/

Docker is client/server

- the server is called the docker daemon (or engine)
- the docker command line utility is a client

### Docker Images

- A Docker image is a read-only template. Images are used to create Docker containers.
- Docker images are the *build* component of Docker.
- Each image consists of a series of layers, starting from a base image (e.g. `ubuntu`)
- A *Dockerfile* contains instructions to build a Docker image
- specified by *repository:tag*, e.g. ubuntu:14.04; default tag is `latest`

### Docker Registries

- Docker registries hold images. The public Docker registry is called Docker Hub.
- Docker registries are the *distribution* component of Docker.
- A registry can hold multiple repositories; the name for the *Official Repositories* is `library`

### Docker Containers

- A Docker container holds everything that is needed for an application to run. Each container is created from a Docker image.
- Docker containers are the *run* component of Docker.
- When Docker runs a container from an image, it adds a read-write layer on top of the image in which your application can then run.

## Docker Hub

docker login

### Useful images

fedora
ubuntu
jboss/wildfly-admin



## Basics



### Info

- `docker info`
- `docker version` displays client and server versions
- `docker images` locally available images ( _base_ or _root_ images like `ubuntu` and _user_ images like `training/webapp`):
        $ docker images
        REPOSITORY       TAG      IMAGE ID      CREATED      VIRTUAL SIZE
        training/webapp  latest   fc77f57ad303  3 weeks ago  280.5 MB
        ubuntu           13.10    5e019ab7bf6d  4 weeks ago  180 MB

### Running containers

- `docker run ubuntu /bin/echo 'Hello World'` quits
- `docker run -it ubuntu bash` is interactive
- `docker run -it ubuntu:14.04 bash` run a specific variant
- `docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`
  daemonize ('detached mode', keep running in background)
- `docker run -e FO_ENV=local -it mycontainer bash` set an environment variable

- Detach ('quit') from an interactive container and keeping it running: Ctrl-P Ctrl-Q (only when the container was run with `-it`)
- `docker reattach` Reattach to a detached container

- `docker exec -it <id> /bin/bash` attaches to a running container, opening a shell

Override stuff

- `docker run -it --entrypoint=/bin/bash mycontainer` override the ENTRYPOINT
- `docker run -it -h myhost mycontainer` override the default HOSTNAME


### Finding Images

- `docker search gcc`


### Dynamic Info

- `docker ps` show running containers
- `docker ps -a` show all containers
- `docker top <id>` show processes
- `docker logs <id>` show output
- `docker inspect <id>` show confg and status info (JSON)
- `docker inspect -f '{{ .NetworkSettings.IPAddress }}' <id>`

### Controlling containers

- `docker pull ubuntu` pre-load an image
- `docker stop <id>` stop a running container politely
  `restart` and `start` do what you expect
- `docker rm <id>` delete a (stopped) container


### Ports and IP Adresses

- `docker port <id>` displays the port mapping
- `docker port <id> 5000` looks up the public-facing port NAT-ed to 5000

- `docker run -P` assigns port automatically (usually > 49152)
- `docker run -p 5000:5000` assigns port explicitly

- with boot2docker the IP address is `boot2docker ip`

### Mapping directories

- `docker run -v /path/host:/path/containers`
- `docker run -w /usr/src/pesche` use `/usr/src/pesche` as working directory inside the container

## Building Images

- Have a `Dockerfile` and possibly other files in a dedicated directory
- `docker build .` in this directory:
        $ docker build .
        ...
        Successfully built 29e2923d226b
        $ docker images
        REPOSITORY                          TAG                 IMAGE ID            CREATED              VIRTUAL SIZE
        <none>                              <none>              29e2923d226b        32 seconds ago       902.4 MB
        ...
- `docker tag <id> foha/devtoolset3` to name (or `tag` an image)
- `docker build -t foha/devtoolset3 .` builds the image and tags it


## Using docker to have a GCC host

### Compiling with docker

- `docker run --rm -v "$PWD":/usr/src/work -w /usr/src/work -it foha/devtoolset3 bash`
- `docker run --rm -v "$PWD":/usr/src/myapp -w /usr/src/myapp foha/devtoolset3 /opt/rh/devtoolset-3/root/bin/gcc -o ici_bienne ici_bienne.c`

### Installing a local RPM into a container

- `docker run -v "$PWD":/usr/src/myapp -it foha/devtoolset3 bash`
  `[root@6bcffaddb3d7 /]# yum --nogpgcheck localinstall /usr/src/myapp/mySoftwarePackage.x86_64.rpm`


## Docker Repositories

docker run -it artifactory.company.net/rhel bash


## Docker Machine

Command line utility `docker-machine`

- needed on Windows/Mac prior to Docker 1.12
- manages the hosts of the Docker Engine (e.g. Virtual Box)
- on Linux useful if you have multiple hosts running Docker Engine

Useful commands

- `docker-machine ls`
  ```
  > docker-machine ls
  NAME      ACTIVE   URL          STATE     URL                         SWARM   DOCKER   ERRORS
  big       *        virtualbox   Running   tcp://192.168.99.101:2376           v1.9.1
  default   -        virtualbox   Running   tcp://192.168.99.100:2376           v1.9.1
  ```
- `docker-machine ip <machine>`
- `docker-machine env <machine>`
- `docker-machine upgrade` to get a newer docker version

If you didn't create machines yourself (e.g. because the default machine has not enough memory allocated),
the `<machine>` name usually is `default`

Example to create a bigger docker machine `machine`:

    docker-machine create --virtualbox-disk-size 20000 --virtualbox-memory 8192 --virtualbox-cpu-count 4 --engine-storage-driver aufs  --engine-env http_proxy=http://10.0.2.2:3128 --engine-env https_proxy=http://10.0.2.2:3128 --engine-env no_proxy="localhost,127.0.0.1,.my-domain.net" --virtualbox-host-dns-resolver --engine-insecure-registry artifactory.my-domain.net -d virtualbox <machine>


## Linux on Mac

boot2docker

docker run -it ubuntu bash
docker run -it fedora bash

