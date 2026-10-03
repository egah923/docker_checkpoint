# 1. Pull nginx
docker pull nginx:latest

# 2. Run nginx
docker run -d \
  --name my-nginx \
  -p 8080:80 \
  nginx:latest

# 3. Check running containers
docker ps

# 4. Enter the container
docker exec -it my-nginx /bin/bash

# Inside the container:
ls -la /usr/share/nginx/html

# Exit
exit

# 5. Restart the container
docker restart my-nginx

# Confirm it is running
docker ps

# Test in browser:
# http://localhost:8080

# 6. Stop and remove container
docker stop my-nginx
docker rm my-nginx

# 7. Remove image
docker rmi nginx:latest