## An arm64 docker image for [mybb](https://github.com/mybb/docker) forum software made by drifty

The official images don't have an arm64 version, and I needed one for my Pi, so I cloned the repo and built the image myself. Useful for anyone with an arm64 processor who wants to run mybb. 

Also available on the GitHub Docker Registry - [```driftywinds/mybb:latest```](https://hub.docker.com/repository/docker/driftywinds/mybb/general)

How to use: - 

1. Create a folder where the compose file and the data directory will be stored.

2. In the directory, use these commands and give access permissions to the "mybb" directory to the webserver: - 

```
sudo touch ./mybb/mybb.sqlite
sudo chown -R www-data:www-data ./mybb
sudo chmod -R 777 ./mybb
```

3. Use this docker file as a template (change values according to your setup): - 

```
services:
  mybb:
    image: driftywinds/mybb:latest
    container_name: mybb
    volumes:
    - ./mybb:/var/www/html

  apache:
    image: php:7.4-apache
    container_name: apache
    ports:
    - '3025:80'
    volumes:
    - ./mybb:/var/www/html
    restart: unless-stopped

version: '3.8'
``` 

4. Type ```docker compose up -d``` and press enter.

5. If this is your first time setting it up, it will ask you the location of the database during initial setup. Just provide it this file - ```./mybb/mybb.sqlite``` 

<br>

You can check logs live with this command: - 
```
docker logs <container name> -f
```
