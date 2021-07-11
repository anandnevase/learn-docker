## Docker Volume

### Create /tmp/index.html
```bash
$ echo  "Hello from Persisten Storage" > /tmp/index.html
```

### Create container by attaching volumes using -v
```bash
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker container run -d -v /tmp:/usr/share/nginx/html/ -p 80:80 --rm nginx:alpine
c53ec2d990ccdfa263288ce763efe712ec606775bdd9ae173ecd1ff9897ec5b5

```

### Access app url
```bash
$ curl http://localhost:80
Hello from Persisten Storage
```
```

### Create Docker volume Mount
```bash
$ docker volume ls
DRIVER    VOLUME NAME

$ docker volume create data
data

$ docker volume ls
DRIVER    VOLUME NAME
local     data

```

### Check Docker volume Mount Details
```bash
$ docker volume inspect data
[
    {
        "CreatedAt": "2021-07-12T01:21:10+05:30",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/data/_data",
        "Name": "data",
        "Options": {},
        "Scope": "local"
    }
]
```

### Start container By attaching Docker volume Mount
```bash
$ docker run -it --name=mount-eg --rm --mount source=data,destination=/data ubuntu
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
c549ccf8d472: Pull complete
Digest: sha256:aba80b77e27148d99c034a987e7da3a287ed455390352663418c0f2ed40417fe
Status: Downloaded newer image for ubuntu:latest

root@8b7aa9055cd8:/# ls
bin  boot  data  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@8b7aa9055cd8:/# cd data/
root@8b7aa9055cd8:/data# ls
root@8b7aa9055cd8:/data# echo "file created from inside container" > file.txt
root@8b7aa9055cd8:/data# pwd
/data
root@8b7aa9055cd8:/data# exit

$ docker run -it --name=mount-eg-2 --rm --mount source=data,destination=/data ubuntu
root@9cbb5c23fa24:/# cat /data/file.txt
file created from inside container
```
