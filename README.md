# SS

## Overview

SAPE.ru scheduler.

## Installation

### Docker

#### Ubuntu

Look here https://docs.docker.com/installation/ubuntulinux/#ubuntu-trusty-1404-lts-64-bit

#### MacOS

Look here https://docs.docker.com/installation/mac/
or
here https://github.com/dduportal/boot2docker-vagrant-box (preffered)

### MySQL container

```sh
docker run -d -p 3306:3306 --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=ss mysql/mysql-server:latest
```

### Gearman container

```sh
docker run -d -p 4731:4371 --name gearman iliyav/gearmand
```

### Redis container

```sh
docker run -d -p 6379:6379 --name redis redis
```

### SS container

```sh
cd <ss project folder>
docker build -t ss docker/
docker run -d -p 8080:80 -p 9001:9001 -v $(pwd):/srv -v ~/.ssh/id_rsa:/root/.ssh/id_rsa --link mysql:mysql --link gearman:gearman --link redis:redis --name=ss -e SYMFONY_ENV=dev ss
```

## Access container shell

```sh
docker exec -it ss /bin/bash
```

## Testing

```sh
docker exec -it ss gulp test
```
