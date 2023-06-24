# Docker Sheet

### What is Docker

Docker is a suite of tools designed to make it easier to create, run and deploy applications in a cross-platform way.

Using Docker we can package our application with all of its dependencies into a single unit, called a container.

This containerized application can be tested and built on a developer's local machine, then easily deployed to any Docker-enabled server without the need to re-test or re-adjust the container to the server environment.

!!! tip

The core idea of Docker comes down to the following concept: develop once, run anywhere”.

#### To Pull Image from docker hub

```bash
docker pull ubuntu
```

## Manage Container & Images

#### Start container

```bash
docker run -p 80:80 --name web nginx
docker run --rm -it -p 5000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
```

#### To Remove Image

```bash
docker image rm nginx
```

#### List of running container

```bash
docker ps
```

#### List of all container

```bash
docker ps -a
```

#### List all the Running Containers with the File Size

```bash
docker container ls -s
```

#### Filter container list

```bash
docker ps -f name=web
```

#### Copy from container to local

```bash
docker cp nosql:/dump ./docker
```

## Copy from local to container

```bash
$ docker cp ./demo/ nosql:/tmp/
```

#### Delete container

```bash
docker rm web
docker rm -f web
```

#### Delete all Containers

```bash
# Delete all the Stopped Containers
docker container prune

# with froce even if the container is running
docker container rm -f $(docker ps -aq)

# without force
docker container rm $(docker ps -aq)

```

#### Kill, Stop, Restart, Pause Container

```bash
docker stop nginx
docker kill nginx
docker restart nginx
docker pause nginx
docker unpause nginx
```

#### Show Images

```bash
docker images
```

#### Delete dangling images

```bash
docker image prune
```

#### Delete all unused Images

```bash
docker image prune -a
```

#### Delete Image

```bash
docker rmi nginx
```

#### Stop container

```bash
docker stop web
```

#### Start a shell inside a container

```bash
docker exec -it web bash
```

#### Start Container in Bash

```bash
docker run -it --name server ubuntu /bin/bash
```

#### Build Image from Dockerfile with tag in current directory

```bash
docker build -t web .
```

#### Save an image to .tar file

```bash
docker save nginx > nginx.tar
```

#### Load an image from a .tar file

```bash
docker load -i nginx.tar
```

## Info & Stats

#### Show the logs of container

```bash
docker log web
```

#### Show stats of running container

```bash
docker stats
```

#### Get Details info about

```bash
docker inspect nginx
```

#### Show all modified files in container

```bash
docker diff nginx
```

#### Show mapped port of the container

```bash
docker port nginx
```

## Clean up

#### Cleans up dangling images, containers, volumes, and networks

```bash
docker system prune
```

#### Remove any stopped containers and all unused images (not just dangling images)

```bash
docker system prune -a
```

## Reference

[Buddy](https://buddy.works/tutorials/docker-commands-cheat-sheet){:target="\_blank"}
