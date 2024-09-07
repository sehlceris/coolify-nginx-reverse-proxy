# coolify-nginx-reverse-proxy

Forked from https://github.com/andreitere/coolify-nginx-reverse-proxy/ and all credit goes to them.

# running on coolify

- Docker Image: `ghcr.io/sehlceris/coolify-nginx-reverse-proxy` Tag: `latest`
- Env Var `PROXY_HOST` set to something like: `http://192.168.1.21:8123`

# running locally

```shell
docker run \
  --rm \
  -e PROXY_HOST=http://192.168.1.21:8123 \
  -p 80:80 \
  --build-arg CONF_TYPE=${CONF_TYPE:-default} \
  ghcr.io/sehlceris/coolify-nginx-reverse-proxy:latest
```

# devving locally

```shell
cp .env.example .env # edit this file to your needs

DOCKER_COMPOSE_FILE=docker-compose-local-test.yaml
docker-compose -f $DOCKER_COMPOSE_FILE; docker-compose -f $DOCKER_COMPOSE_FILE up
```