# Docker Swarm

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
