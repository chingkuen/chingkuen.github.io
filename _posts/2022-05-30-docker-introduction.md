---
layout: post
title: Docker Instruction
subtitle: Docker Instruction
categories: docker
tags: [docker]
---

# Docker

- Image 映像檔

- Container 容器

- Repository 倉庫

## Install Docker

```Linux
sudo apt install docker.io
```

## Download Image from Docker Hub repository

```Linux
docker pull [repository address]:[port]/[Image 名稱]:[Image 版本]
```

## Start Container

```Linux
docker run -i -t [Image 名稱]:[Image 版本] [執行指令]
```

- -i, --interactive (互動模式)

- -t, --tty         (配置一個終端機)

- -d, --detach      (在背景執行)

### Quit from container

1. Enter "exit", the container will be stopped
2. Press ctrl+P, then ctrl+Q, the container will continue working

## List Local Images

```Linux
docker images
```

### Remove the Image

```Linux
docker rmi [Image ID]
```

## Commit New Image

After changing the container

```Linux
docker commit -m <commit message> -a <user update message> <container ID> <repository>/<image name>:<tag>
```

## Attach the running container

```Linux
docker ps
docker exec -i -t [Container ID] bash
exit
```

### Start the container

```Linux
docker start [Container ID]
```

### Stop the container

```Linux
docker stop [Container ID]
```

### Restart the container

```Linux
docker restart [Container ID]
```

### Remove the container

```Linux
docker rm [Container ID]
```
