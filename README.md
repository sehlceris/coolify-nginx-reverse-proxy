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

# NOTE

This repository is now obsolete for me, because I figured out how to use `nginx-proxy-manager` within coolify.

```
- create a new project/resource named nginx-proxy-manager
- docker image: jc21/nginx-proxy-manager | tag: latest
- domains: https://yourservice.yourdomain.com,https://nginx-proxy-manager.yourdomain.com:81
- note: the :81 is important since that will hit nginx-proxy-manager's admin port
- make sure your DNS for all those domains is pointed to your Coolify server
- add storage: name: "data" | destination path: "/data"
- add storage: name: "letsencrypt" | destination path: "/etc/letsencrypt"
- deploy
- visit https://nginx-proxy-manager.yourdomain.com (do not add any port afterward)
- default login is admin@example.com / changeme
- go to hosts tab -> proxy hosts
- add a proxy host
- domain names: yourservice.yourdomain.com
- scheme: http (coolify will take care of https, so nginx proxy manager is out of that chain)
- forward hostname/ip/port: whatever you want to proxy pass to, e.g. 192.168.1.21:8123
- enable websockets/block common exploits if you wish
- save. done.

references: https://nginxproxymanager.com/guide/
```