# 03 - Docker Volumes

## Create a named volume

```bash
docker volume create mysql-data
```

## Run MySQL with a persistent volume

```bash
docker run -d \
  --name mysql-vol \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=myappdb \
  -v mysql-data:/var/lib/mysql \
  -p 3306:3306 \
  mysql:8.0
```

## Insert sample data

```bash
docker exec -it mysql-vol mysql -uroot -prootpass -e "
CREATE TABLE IF NOT EXISTS users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50));
INSERT INTO users (name) VALUES ('Alice'), ('Bob');
SELECT * FROM users;
"
```

## Stop, remove, and restart container to confirm persistence

```bash
docker stop mysql-vol
docker rm mysql-vol

docker run -d \
  --name mysql-vol \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=myappdb \
  -v mysql-data:/var/lib/mysql \
  -p 3306:3306 \
  mysql:8.0

docker exec mysql-vol mysql -uroot -prootpass -e "SELECT * FROM users;"
```
