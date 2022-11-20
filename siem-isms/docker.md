# Docker

```
docker start $(docker images; awk '{print $1}'; cut -d "/" -f3)
```

`docker ps -a` see all containers

`docker images` see all images
