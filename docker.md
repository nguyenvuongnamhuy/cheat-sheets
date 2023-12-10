# Table of Contents

- [Docker file](#docker-file)
  - [Build](#build)
  - [Run](#run)
- [Docker compose](#docker-compose)
  - [Run](#run-1)
  - [Stop](#stop)
  - [Down](#down)
  - [Restart](#restart)
- [Docker commands](#docker-commands)
  - [Version](#version)
  - [Search](#search)
  - [Pull image](#pull)
  - [Image](#image)
    - [Listing](#listing)
    - [Remove](#remove)
    - [Import](#import)
    - [Export](#export)
  - [Container](#container)
    - [Listing](#listing-1)
    - [Remove](#remove-1)
    - [Stop](#stop-1)
    - [Access into container](#access-into-container)
    - [Show logs](#show-logs)
  - [Volume](#volume)
    - [Remove all unused local volumes](#remove-all-unused-local-volumes)
  - [Private network](#private-network)
    - [Listing all networks](#listing-all-networks)
    - [Create network](#create)
    - [Run containers](#run-container-in-private-network)

# Docker file

## Build

```bash
docker build . -t ${IMAGE_NAME}
```

Build on specific name

```bash
docker build -f ${DOCKER_FILE} . -t ${IMAGE_NAME}
```

## Run

```bash
docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}
```

Run with environment variables and allow limited connections

```bash
docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME} -e ${ENV_KEY}=${ENV_VALUE} --max_connections=${NUMBER}
```

Or with .env file

```bash
docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME} --env-file ./.env
```

# Docker compose

## Run

Only build for the first time

```bash
docker compose up -d
```

Build every run

```bash
docker compose up -d --build
```

Run with specific compose files

```bash
docker-compose -f ${DOCKER_COMPOSE_1}.yml -f ${DOCKER_COMPOSE_2}.yml up -d
```

## Stop

```bash
docker compose stop
```

## Down

```bash
docker compose down
```

## Restart

```bash
docker compose restart
```

# Docker commands

## Version

```bash
docker -v
```

## Search

```bash
docker search ${SERVICE_NAME}
```

## Pull

```bash
docker pull ${SERVICE_NAME}
```

## Copy file into container

```bash
docker cp /path ${CONTAINER_NAME}:/path
```

## Image

### Listing

```bash
docker images -a
docker image ls
```

#### Remove

```bash
docker rmi -f ${IMAGE_NAME}
```

Remove all images

```bash
docker rmi -f $(docker images -q)
```

### Import

```bash
docker load < ${FILE_NAME}.tar
docker load -i ${FILE_NAME}.tar
```

### Export

```bash
docker save ${IMAGE_NAME} > ${FILE_NAME}.tar
docker save -o ${FILE_NAME}.tar ${IMAGE_NAME}
```

## Container

### Listing

```bash
docker ps -a
docker container ls
```

### Remove

```bash
docker rm -f ${CONTAINER_NAME}
```

Remove all containers

```bash
docker rm -f $(docker ps -aq)
```

### Stop

```bash
docker stop ${CONTAINER_NAME}
```

### Access into container

```bash
docker exec -it ${CONTAINER_NAME} bash
docker exec -it ${CONTAINER_NAME} sh
```

### Show logs

```bash
docker logs -f ${CONTAINER_NAME}
docker logs -f ${CONTAINER_NAME} --tail ${NUMBER}
```

## Volume

### Remove all unused local volumes

```bash
docker volume prune
```

## Private network

### Listing all networks

```bash
docker network ls
```

### Create

```bash
docker network create ${NETWORK_NAME}
```

### Run container in private network

```bash
docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME} --net ${NETWORK_NAME}
```

---
