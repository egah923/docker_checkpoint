# 04 - Docker Networking

## Create a custom bridge network

```bash
docker network create app-net
```

## Run containers on the same network

```bash
docker run -d --name app-one --network app-net python:3.12-alpine sleep 300
docker run -d --name app-two --network app-net python:3.12-alpine sleep 300
```

## Test name-based communication

```bash
docker exec app-one ping -c 2 app-two
```

## Run a web service inside the network

```bash
docker run -d --name web-server --network app-net -p 8000:8000 web-app:latest
```

Then from another container:

```bash
docker exec app-one wget -qO- http://web-server:8000
```
