# Docker Checkpoint

This project is organized as a Docker learning checkpoint. Each folder contains a focused exercise covering one Docker concept.

## Project structure

```text
docker-checkpoint/
├── README.md
├── 01-docker-basics/
│   └── commands.md
├── 02-dockerfile/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
├── 03-volumes/
│   └── commands.md
├── 04-networking/
│   ├── app.py
│   ├── Dockerfile
│   └── commands.md
├── 05-compose/
│   ├── docker-compose.yml
│   ├── backend/
│   │   ├── Dockerfile
│   │   ├── app.py
│   │   └── requirements.txt
│   └── nginx/
│       └── nginx.conf
└── README.md
```


## Topics covered

1. Docker basics and CLI commands
2. Dockerfile creation and image building
3. Docker volumes and persistence
4. Networking between containers
5. Docker Compose multi-service deployment

## 1. Docker basics

Open the file [01-docker-basics/commands.md](01-docker-basics/commands.md) for the exercises.

Common commands:

```bash
docker --version
docker pull nginx:latest
docker run -d --name nginx-demo -p 8080:80 nginx:latest
docker ps
docker exec -it nginx-demo /bin/bash
docker stop nginx-demo
docker rm -f nginx-demo
```

---

## 2. Dockerfile

The Dockerfile example is in [02-dockerfile/Dockerfile](02-dockerfile/Dockerfile).

Build and run it:

```bash
cd 02-dockerfile
docker build -t my-python-app:v1 .
docker run -d --name my-python-app -p 5000:5000 my-python-app:v1
curl http://localhost:5000
```

Expected output:

```text
Hello from Dockerfile app!
```

---

## 3. Volumes

The volume exercise is in [03-volumes/commands.md](03-volumes/commands.md).

Main idea:

- create a named Docker volume
- mount it to MySQL
- insert data
- restart the container
- confirm that the data still exists

```bash
docker volume create mysql-data
docker run -d --name mysql-vol -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=myappdb -v mysql-data:/var/lib/mysql -p 3306:3306 mysql:8.0
```

---

## 4. Networking

The networking example is in [04-networking/commands.md](04-networking/commands.md).

Create a custom bridge network and test container-to-container communication:

```bash
docker network create app-net
docker run -d --name app-one --network app-net python:3.12-alpine sleep 300
docker run -d --name app-two --network app-net python:3.12-alpine sleep 300
docker exec app-one ping -c 2 app-two
```

---

## 5. Docker Compose

The compose stack is in [05-compose/docker-compose.yml](05-compose/docker-compose.yml).

Run the stack:

```bash
cd 05-compose
docker compose up -d --build
curl http://localhost:8081
```

Expected output:

```text
Hello from Flask backend!
```

Check the services:

```bash
docker compose ps
docker compose logs
```

---

## Useful tips

- Use `docker ps -a` to see all containers.
- Use `docker logs <container_name>` when debugging.
- Use `docker rm -f <container_name>` to clean up stopped containers.
- Use `docker compose down` to stop and remove the compose environment.

## Cleanup

```bash
docker compose down
docker system prune -f
```

This project is intended as a practical checkpoint for understanding Docker fundamentals in a simple, reproducible setup.
