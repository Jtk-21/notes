# Docker

```
docker start $(docker images; awk '{print $1}'; cut -d "/" -f3)
```
