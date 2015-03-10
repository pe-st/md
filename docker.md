docker
======

## Meta

Note: if you are using a remote Docker daemon, such as Boot2Docker, then do not type the sudo before the docker commands shown in the documentation's examples.


## Docker Hub

docker login


## Basics

### Running containers

- `docker run ubuntu /bin/echo 'Hello World'` quits
- `docker run -it ubuntu bash` is interactive
- `docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`
  daemonize (keep running in background)

### Info

- `docker info`
- `docker version`
- `docker ps` show running containers
- `docker top <id>` show processes
- `docker logs <id>` show output
- `docker inspect <id>` show confg and status info (JSON)


### Controlling containers

- `docker stop <id>` stop a running container politely


### Ports and IP Adresses

- `-P` assigns port automatically (usually > 49152)

- with boot2docker the IP address is `boot2docker ip`




## Linux on Mac

boot2docker

docker run -it ubuntu bash
docker run -it fedora bash

