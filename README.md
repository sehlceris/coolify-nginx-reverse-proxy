# testing locally

```shell
cp .env.example .env # edit this file to your needs

DOCKER_COMPOSE_FILE=docker-compose-local-test.yaml
docker-compose -f $DOCKER_COMPOSE_FILE; docker-compose -f $DOCKER_COMPOSE_FILE up
```

# running from github registry

TODO