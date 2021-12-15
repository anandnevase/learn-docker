## Docker Compose

### Install docker Compose
```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

$ docker-compose --version
docker-compose version 1.26.2, build 1110ad01
```

### Start Multicontainer from docker-compose
```bash
$ docker-compose up -d
```

### docker-compose Image
```bash
$ docker-compose images
```

### Stop containers
```bash
$ docker-compose stop

```

### Start only one container
```bash
$ docker-compose run db -d
```

### Start all containers
```bash
$ docker-compose up -d
```

### Check all containers
```bash
$ docker-compose ps 
```

### Scale up/down container
```bash
$  docker-compose scale --help
$  docker-compose scale wordpress=2
$  docker-compose scale db=2
$  docker-compose ps
$  docker-compose scale db=1
```


### Remove all containers
```bash
$ docker-compose down
```