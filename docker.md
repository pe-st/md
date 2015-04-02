docker
======

## Meta

Note: if you are using a remote Docker daemon, such as Boot2Docker, then do not type the sudo before the docker commands shown in the documentation's examples.

Artifactory has docker extension


## Docker Hub

docker login

### Useful images

fedora
ubuntu
jboss/wildfly-admin



## Basics

### Info

- `docker info`
- `docker version`
- `docker images` locally available images

### Running containers

- `docker run ubuntu /bin/echo 'Hello World'` quits
- `docker run -it ubuntu bash` is interactive
- `docker run -it ubuntu:14.04 bash` run a specific variant
- `docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`
  daemonize (keep running in background)

### Dynamic Info

- `docker ps` show running containers
- `docker top <id>` show processes
- `docker logs <id>` show output
- `docker inspect <id>` show confg and status info (JSON)
- `docker inspect -f '{{ .NetworkSettings.IPAddress }}' <id>`

### Controlling containers

- `docker pull ubuntu` pre-load an image
- `docker stop <id>` stop a running container politely
  `restart`and `start` do what you expect
- `docker rm <id>` delete a (stopped) container


### Ports and IP Adresses

- `docker port <id>` displays the port mapping
- `docker port <id> 5000` looks up the public-facing port NAT-ed to 5000

- `docker run -P` assigns port automatically (usually > 49152)
- `docker run -p 5000:5000` assigns port explicitly

- with boot2docker the IP address is `boot2docker ip`




## Linux on Mac

boot2docker

docker run -it ubuntu bash
docker run -it fedora bash

