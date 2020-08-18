# Docker

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
