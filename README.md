
# Supported tags and respective Dockerfile links
[v7.9](https://github.com/creecros/resourcespace-docker/blob/v7.9/Dockerfile)

[v8.0](https://github.com/creecros/resourcespace-docker/blob/v8.0/Dockerfile)

[v8.1](https://github.com/creecros/resourcespace-docker/blob/v8.1/Dockerfile)

[v8.2](https://github.com/creecros/resourcespace-docker/blob/v8.2/Dockerfile)

[v8.3](https://github.com/creecros/resourcespace-docker/blob/v8.3/Dockerfile)

[v8.4](https://github.com/creecros/resourcespace-docker/blob/v8.4/Dockerfile)

[v8.5](https://github.com/creecros/resourcespace-docker/blob/v8.5/Dockerfile)

[v8.6](https://github.com/creecros/resourcespace-docker/blob/v8.6/Dockerfile)


# ResourceSpace Docker Container
ResourceSpace running on Apache2 Docker Container Built on phusion/baseimage

## Example usage:
```
docker run -p 80:80 \
creecros/resourcespace-docker:v8.3
```
```
docker run -p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=Un1C0rn \
-e MYSQL_DATABASE=resourcespace \
mysql:5.6
```

*Do not use with latest Mysql, use 5.6

To create volumes on the host, create the volumes with docker volume create

In resourcespace Installation, seem to not be able to specify a port, so either map to 3306 or use the private IP during install.

designate your path: `/mnt/to/your/path`

## docker-compose example
```
version: '2'
services:
  resourcespace:
    image: creecros/resourcespace-docker:latest
    stdin_open: true
    network_mode: bridge
    tty: true
    ports:
      - 80:80/tcp
    volumes:
      - include:/include
      - filestore:/filestore
  mysql-resourcespace:
    image: mysql:5.6
    environment:
      MYSQL_DATABASE: resourcespace
      MYSQL_ROOT_PASSWORD: Un1c0rn
    stdin_open: true
    network_mode: bridge
    tty: true
    ports:
      - 3306:3306/tcp

volumes:
  filestore:
    driver: local
    driver_opts:
      type: none
      device: /mnt/to/your/path
      o: bind
  include:
    driver: local
    driver_opts:
      type: none
      device: /mnt/to/your/path
      o: bind
  ```
