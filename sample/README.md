# Sample


## local

```bash


docker build -t ragna/sample .
docker tag  ragna/sample localhost:5000/ragna/sample
docker push localhost:5000/ragna/sample
docker run -d -p 8090:8081 ragna/sample:latest

http http://localhost:5000/v2/_catalog
http http://localhost:5000/v2/ragna/sample/tags/list



```

## Web Server Build

```bash

$ export NP_PORT=15873


$ export DOCKER_HOST="tcp://build.swarm.devfactory.com"

$ docker build -t registry2.swarm.devfactory.com/ragna/sample:latest .

$ docker push registry2.swarm.devfactory.com/ragna/sample:latest


####  registry swarm build

docker login -u njunior registry2.swarm.devfactory.com
#docker tag  ragna/sample:latest registry2.swarm.devfactory.com/ragna/sample:latest
docker push registry2.swarm.devfactory.com/ragna/sample:latest


 http https://registry2.swarm.devfactory.com/v2/_catalog

 http https://registry2.swarm.devfactory.com/v2/ragna/sample/tags/list


```

## Web Server deploy

```bash

$ export DOCKER_HOST="tcp://webserver.devfactory.com"

$ docker service create \
-p $NP_PORT:8081 \
--name codefix_npaurea_sample \
--replicas 1 \
--limit-cpu 2 \
--limit-memory 128M \
--label owner.email="nilseu.junior@aurea.com" \
registry2.swarm.devfactory.com/ragna/sample:latest

# Cannot connect to the Docker daemon at tcp://webserver.devfactory.com:2375. Is the docker daemon running?

$ docker ps -f "label=owner.email=nilseu.junior@aurea.com"
$ docker ps --filter status=running

```


## X1 Host

```bash

$ export DOCKER_HOST="tcp://x1.devfactory.com"

$ dig x1.devfactory.com
# 10.69.11.89

$ docker run -d --name codefix_npaurea_sample \
-m 32m \
--cpu-quota 300000 \
--cpu-period=50000 \
--label owner.email="nilseu.junior@aurea.com" \
--label com.trilogy.company="aurea" \
--label com.trilogy.stage="dev" \
-p $NP_PORT:8081 \
registry2.swarm.devfactory.com/ragna/sample:latest



#  docker ps --filter  "name=codefix_npaurea_sample"
#CONTAINER ID        IMAGE                                                COMMAND                  CREATED             STATUS              PORTS                         NAMES
# deccfab38cb2        registry2.swarm.devfactory.com/ragna/sample:latest   "nodejs # /var/www/app…"   11 seconds ago      Up 9 seconds        10.69.11.89:16605->8081/tcp   codefix_npaurea_sample


$ docker ps --filter "label=owner.email=nilseu.junior@aurea.com"
$ docker ps --filter status=running
$ docker ps --filter "name=codefix_npaurea_sample"


$ docker ps -a --filter  "status=exited"
$ docker ps -a -f  "name=codefix_npaurea_sample"
$ docker ps -a --filter "label=owner.email=nilseu.junior@aurea.com"


$ docker ps -a --filter "label=owner.email=nilseu.junior@aurea.com" --format "{{.ID}}: {{.Command}} : {{.Names}} : {{.Status}}"

#16d021143a17: "nodejs /var/www/app…" : codefix_npaurea_sample : Exited (137) 45 seconds ago


# http://tldp.org/LDP/abs/html/exitcodes.html
# https://github.com/moby/moby/issues/22211 (OOM KILLER)
```

$ docker logs --timestamps codefix_npaurea_sample
