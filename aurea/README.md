# Commands



# Traefik

```
$ export DOCKER_HOST="tcp://build.swarm.theserver.com"

$ docker run -d --name traefik-npaurea-plain-1 -m 1024m --cpu-shares 100000 -l "traefik.port=80" -l "traefik.protocol=http" -l "traefik.enable=true" -l "traefik.backend=npaurea-plain" nginx:alpine

$ http https://traefik-npaurea-plain-1.central.aurea.local

$ http build.swarm.theserver.com Host:traefik-npaurea-plain-1

$ http build.swarm.theserver.com:8080 Host:traefik-npaurea-plain-1

$ docker run -d --name traefik-npaurea-plain-2 -m 1024m --cpu-shares 100000 -l "traefik.port=80" -l "traefik.protocol=http" -l "traefik.enable=true" -l "traefik.backend=npaurea-plain" nginx:alpine

$ http https://traefik-npaurea-plain-2.central.aurea.local

$  docker run -d --name traefik-npauread-1 -m 1024m --cpu-shares 100000 -l "traefik.port=80" -l "traefik.protocol=http" -l "traefik.enable=true" -l "traefik.backend=npaurea.testing.my" -l "traefik.frontend.rule=Host:npaurea.testing.my" nginx:alpine

$ http https://npaurea.testing.my


```


# docker image

``` bash
$ docker build -t npaurea:latest .

$ docker login -u njunior registry2.swarm.theserver.com

$ docker tag npaurea:latest registry2.swarm.theserver.com/codefix/npaurea:latest

$ docker push registry2.swarm.theserver.com/codefix/npaurea:latest


$ docker run -d --name testcontainer-npauread-1 \ 
-m 1024m --cpu-shares 100000 \
-l "com.trilogy.company=aurea" \
-l "com.trilogy.product=node" \
-l "com.trilogy.service=npauread" \
-l "com.trilogy.stage=dev" \
-l "com.trilogy.maintainer.skype=ragnarokkrr" \
-l "com.trilogy.maintainer.email=nilseu.junior@aurea.com" \
# -p 10.69.11.211:28401:8080 \
-p build.swarm.theserver.com::8081

```


