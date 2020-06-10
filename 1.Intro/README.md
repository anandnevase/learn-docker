## Basic Docker Command

### 1. Check Docker Engine Running 
```bash
$ ps -ef | grep docker
root         156       1  0 05:35 ?        00:00:00 /usr/bin/dockerd -p /var/run/docker.pid --mtu=1460 --registry-mirror=https://asia-mirror.gcr.io
root         176     156  0 05:35 ?        00:00:00 containerd --config /var/run/docker/containerd/containerd.toml --log-level info
nevase_+     517     377  0 05:37 pts/3    00:00:00 grep --color=auto docker
```
### 2. List Docker Images availabe locally
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```
### 3. Download Hello World image
```bash
$ docker pull hello-world

Using default tag: latest
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:6a65f928fb91fcfbc963f7aa6d57c8eeb426ad9a20c7ee045538ef34847f44f1
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
```
### 4. Check Hello World Image Locally
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        5 months ago        13.3kB
```
### 5. Run Hello World Image    
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

### 6. Practice command to check operating images 
```bash
$ docker run -ti --name container1 centos  cat /etc/os-release

$ docker run -ti --name container1 centos:7  cat /etc/os-release

$ docker run -ti --name container1 ubtunu  cat /etc/os-release

```