# Sample



```
docker build -t ragna/sample .
docker tag  ragna/sample localhost:5000/ragna/sample
docker push localhost:5000/ragna/sample

docker run -d -p 8090:8081 ragna/sample:latest
```