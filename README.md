# Docker Cheatsheet

The main idea of this repository is to teach the basic principles of working with Docker using the required commands. A prime example is to create a simple Dockerfile and docker-compose.

## Docker

**Usage:**  docker [OPTIONS] COMMAND

```
docker --help
docker run <image>
docker run --name=image_name <image>
docker run -d <image>
docker run <image>:<tag_name> (default :latest)
docker run -i <image>
docker run -p 80:5000 <image>
docker run -e "ENV_NAME=VALUE" <image>
docker run -v <volume_name>:<container_path>
docker ps
docker ps -a
docker stop <container>
docker rm <container>
docker images
docker rmi <image>
docker pull <image>
docker exec <command>
docker attach <image>
docker cp <container>:<container_path> <host_path>
docker cp <host_path> <container>:<container_path>
docker inspect <container>
docker logs <container>
docker volume ls
docker volume create <volume_name>
docker push <tag_name>
```

**Examples**

- docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Pass@Word1" -p 21143:1433 --name sql19-23t -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CU5-ubuntu-18.04
- docker cp conatiner:/var/opt/mssql/data/ C:\docker



## Dockerfile

**Usage:**  docker build Dockerfile -t tag_name

```
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/Masny.WebApi/Masny.WebApi.csproj", "src/Masny.WebApi/"]
RUN dotnet restore "src/Masny.WebApi/Masny.WebApi.csproj"
COPY . .
WORKDIR "/src/src/Masny.WebApi"
RUN dotnet build "Masny.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Masny.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Masny.WebApi.dll"]
```

**.dockerignore**

```
**/.classpath
**/.dockerignore
**/.env
**/.git
**/.gitignore
**/.project
**/.settings
**/.toolstarget
**/.vs
**/.vscode
**/*.*proj.user
**/*.dbmdl
**/*.jfm
**/azds.yaml
**/bin
**/charts
**/docker-compose*
**/Dockerfile*
**/node_modules
**/npm-debug.log
**/obj
**/secrets.dev.yaml
**/values.dev.yaml
LICENSE
README.md
```



## Docker compose (docker-compose.yml)

**Usage:**  docker-compose up

```
version: '3.4'

services:
  masny.webapi:
    image: ${DOCKER_REGISTRY-}masnywebapi
    build:
      context: .
      dockerfile: src/Masny.WebApi/Dockerfile
    ports:
    - 80:80
    - 443:443
```

```
version: '2.0'

services:
  redis:
    image: redis
    networks:
      - back-end
  db:
    image: postgres:9.4
    networks:
      - back-end
  vote:
    image: voting-app
    networks:
      - front-end
      - back-end
  result:
    image: result
    networks:
      - front-end
      - back-end
networks:
  front-end:
  back-end:
```



## Docker registry

`image: docker.io/nginx/nginx`, where:
- docker.io : registry
- nginx : user or account
- nginx : image or repository



## Docker Swarm

**Usage:**  docker swarm COMMAND

```
docker swarm init
docker swarm join-token manager
docker swarm join-token worker
docker swarm join --token <token>
docker service create --replicas=<count> -p <out:in> <image>
docker service ls
docker service rm <image>
```



## Kubernetes

```
kubectl run --replicas=<count> <image>
kubectl scale --replicas=<count> <image>
kubectl rolling-update <image> --image=<new_image>
kubectl roling-update <image> --rollback
```
