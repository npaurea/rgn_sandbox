# Traefik

* [Traefik](https://docs.traefik.io/)

```

$ docker-compose up -d reverse-proxy

$ docker-compose up -d whoami

$ curl -H Host:whoami.docker.localhost http://127.0.0.1


```