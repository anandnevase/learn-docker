## Docker Image Command


### List Docker Images availabe locally
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

### 3. Download Hello World image
```bash
$ docker image pull hello-world

Using default tag: latest
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:6a65f928fb91fcfbc963f7aa6d57c8eeb426ad9a20c7ee045538ef34847f44f1
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
```
### Check Hello World Image Locally
```bash
$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        5 months ago        13.3kB
```
### Run Hello World Image    
```bash
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

```
### Remove Image locally   
```bash
$ docker image ls
REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
hello-world                 latest    d1165f221234   4 months ago   13.3kB
fhsinchy/hello-dock         latest    f540930e8157   5 months ago   21.9MB
centos                      latest    300e315adb2f   7 months ago   209MB
openshift/hello-openshift   latest    7af3297a3fb4   3 years ago    6.09MB

$ docker image rm d1165f221234
Untagged: hello-world:latest
Untagged: hello-world@sha256:df5f5184104426b65967e016ff2ac0bfcd44ad7899ca3bbcf8e44e4461491a9e
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
```

### Remove un-tagged dangling images 
```bash
# docker image prune --force

Deleted Images:
deleted: sha256:ba9558bdf2beda81b9acc652ce4931a85f0fc7f69dbc91b4efc4561ef7378aff
deleted: sha256:ad9cc3ff27f0d192f8fa5fadebf813537e02e6ad472f6536847c4de183c02c81
deleted: sha256:f1e9b82068d43c1bb04ff3e4f0085b9f8903a12b27196df7f1145aa9296c85e7
deleted: sha256:ec16024aa036172544908ec4e5f842627d04ef99ee9b8d9aaa26b9c2a4b52baa

Total reclaimed space: 59.19MB
```

### Practice command to check operating images 
```bash
$ docker container run -ti --name container1 centos  cat /etc/os-release

$ docker container run -ti --name container1 centos:7  cat /etc/os-release

$ docker container run -ti --name container1 ubtunu  cat /etc/os-release
```