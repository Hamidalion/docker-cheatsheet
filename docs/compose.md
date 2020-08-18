# Docker compose (docker-compose.yml)

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
