## Docker Container Command

### Check Docker Engine Running 
```bash
$ service docker status
Redirecting to /bin/systemctl status docker.service
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://docs.docker.com

# Start Docker Engine
$ service docker start
Redirecting to /bin/systemctl start docker.service
$ service docker status
Redirecting to /bin/systemctl status docker.service
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: active (running) since Sun 2021-07-11 19:00:33 IST; 12s ago
     Docs: https://docs.docker.com
 Main PID: 27326 (dockerd)
    Tasks: 16
   Memory: 48.8M
   CGroup: /system.slice/docker.service
           └─27326 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Jul 11 19:00:32 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:32.730739520+05:30" level=info msg="scheme \"un...=grpc
Jul 11 19:00:32 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:32.730780651+05:30" level=info msg="ccResolverW...=grpc
Jul 11 19:00:32 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:32.730812045+05:30" level=info msg="ClientConn ...=grpc
Jul 11 19:00:32 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:32.756663219+05:30" level=info msg="Loading con...art."
Jul 11 19:00:32 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:32.906908306+05:30" level=info msg="Default bri...ress"
Jul 11 19:00:32 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:32.978594778+05:30" level=info msg="Loading con...one."
Jul 11 19:00:33 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:33.017854906+05:30" level=info msg="Docker daem....10.7
Jul 11 19:00:33 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:33.018215866+05:30" level=info msg="Daemon has ...tion"
Jul 11 19:00:33 10_1_10_6.corpacademia.net systemd[1]: Started Docker Application Container Engine.
Jul 11 19:00:33 10_1_10_6.corpacademia.net dockerd[27326]: time="2021-07-11T19:00:33.062367785+05:30" level=info msg="API listen ...sock"
Hint: Some lines were ellipsized, use -l to show in full.
```


### Run Hello World Image    
```bash
$ docker container run hello-world 
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:df5f5184104426b65967e016ff2ac0bfcd44ad7899ca3bbcf8e44e4461491a9e
Status: Downloaded newer image for hello-world:latest

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

### Check Hello World Image Locally
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        5 months ago        13.3kB
```

### Check docker Process
```bash
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker container ls -a
CONTAINER ID   IMAGE         COMMAND    CREATED              STATUS                          PORTS     NAMES
797b5f69b06d   hello-world   "/hello"   About a minute ago   Exited (0) About a minute ago             beautiful_leavitt
```

### Check docker inspect
```bash
$ docker inspect hello-world
```

### Rename Container name
```bash
$ docker container rename beautiful_leavitt hello-world
$ docker container ls -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
797b5f69b06d   hello-world   "/hello"   6 minutes ago   Exited (0) 6 minutes ago             hello-world
```

### Run Web Container in detach mode (run in background)
```bash
$ docker container run -d -p 8080:8080 openshift/hello-openshift
Unable to find image  'openshift/hello-openshift:latest' locally
latest: Pulling from openshift/hello-openshift
4f4fb700ef54: Pull complete
8b32988996c5: Pull complete
a639213bd49031939620ad48dc6af257eff6827a7f5b8ae9183e658c861788c7

$ docker container ls
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS         PORTS                                                 NAMES
a639213bd490   openshift/hello-openshift   "/hello-openshift"   10 seconds ago   Up 9 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 8888/tcp   ecstatic_darwin
```

### Stop & Kill Container
```bash
$ docker container stop a639213bd490
a639213bd490
$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
$ docker container ls -a
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS                      PORTS     NAMES
a639213bd490   openshift/hello-openshift   "/hello-openshift"   3 minutes ago    Exited (2) 9 seconds ago              ecstatic_darwin
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   8 minutes ago    Exited (2) 7 minutes ago              admiring_mayer
797b5f69b06d   hello-world                 "/hello"             18 minutes ago   Exited (0) 18 minutes ago             hello-world
$ docker container rm a639213bd490
a639213bd490
$ docker container ls -a
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS                      PORTS     NAMES
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   8 minutes ago    Exited (2) 8 minutes ago              admiring_mayer
797b5f69b06d   hello-world                 "/hello"             19 minutes ago   Exited (0) 19 minutes ago             hello-world
```

### Restart container
```bash
$ docker container ls -a
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS                      PORTS     NAMES
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   9 minutes ago    Exited (2) 9 minutes ago              admiring_mayer
797b5f69b06d   hello-world                 "/hello"             20 minutes ago   Exited (0) 20 minutes ago             hello-world
$ docker container start 78fea4c74652
78fea4c74652
$ docker container ls -a
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS                      PORTS                NAMES
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   9 minutes ago    Up 2 seconds                8080/tcp, 8888/tcp   admiring_mayer
797b5f69b06d   hello-world                 "/hello"             20 minutes ago   Exited (0) 20 minutes ago                        hello-world
```

### Remove Dangling Containers
```bash
$ docker container ls
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS         PORTS                NAMES
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   12 minutes ago   Up 3 minutes   8080/tcp, 8888/tcp   admiring_mayer
$ docker container ls -a
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS                      PORTS                NAMES
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   13 minutes ago   Up 3 minutes                8080/tcp, 8888/tcp   admiring_mayer
797b5f69b06d   hello-world                 "/hello"             23 minutes ago   Exited (0) 23 minutes ago                        hello-world
$ docker container rm 797b5f69b06d
797b5f69b06d
$ docker container ls -a
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS         PORTS                NAMES
78fea4c74652   openshift/hello-openshift   "/hello-openshift"   13 minutes ago   Up 3 minutes   8080/tcp, 8888/tcp   admiring_mayer
$ docker container rm admiring_mayer
Error response from daemon: You cannot remove a running container 78fea4c74652bfdd0f1b323e9cd0b3509acb9d86e96e3d84c4bbd343c39b7915. Stop the container before attempting removal or force remove
$ docker container rm -f admiring_mayer
admiring_mayer
$ docker container ls -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### Configure Container to remove as soon as its stops  
```bash
$ docker container run --rm -d -p 8080:8080 openshift/hello-openshift
db7b55e60d8d825997a7b420a8e44097fe5a0bfca9b4d3a96d384f0d2e119cd1
$ docker container ls
CONTAINER ID   IMAGE                       COMMAND              CREATED         STATUS         PORTS                                                 NAMES
db7b55e60d8d   openshift/hello-openshift   "/hello-openshift"   7 seconds ago   Up 6 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 8888/tcp   zealous_bardeen
$ docker container stop db7b55e60d8d
db7b55e60d8d
$ docker container ls -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### Run a Container in Interactive Mode
```bash
$ docker container run --rm -it ubuntu

$ root@dbb1f56b9563:/# cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.1 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.1 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

### How to Execute Commands Inside a Container
```bash
$ docker container run alpine uname -a
# Linux f08dbbe9199b 5.8.0-22-generic #23-Ubuntu SMP Fri Oct 9 00:34:40 UTC 2020 x86_64 Linux
```


### Configuring Docker container to restart even if Docker-Engine(daemon)/machine is rebooted, using --restart=always option
```bash
$ docker container run -it --name httpd-restart --restart always -d -p 9090:80 httpd
646a81d5d8a4883b2072a05dec7ef9887d54bfeb95ee3fdd1fc0b5f83bb790bd

$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
646a81d5d8a4        httpd               "httpd-foreground"   5 seconds ago       Up 4 seconds        0.0.0.0:9090->80/tcp   httpd-restart

$ sudo service docker restart
Stopping Docker: docker.
Starting Docker: docker.

$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
646a81d5d8a4        httpd               "httpd-foreground"   33 seconds ago      Up 5 seconds        0.0.0.0:9090->80/tcp   httpd-restart
```

### Configuring Docker container to restart automatic on failure 
```bash
$ docker container ls -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
$ docker container run -d -p 8080:8080 --restart=always openshift/hello-openshift
f0d91de758a65a22f30ef80bc2aaa4b7ad409c38c458b778eacc3194e171d0f1
$ docker container ls
CONTAINER ID   IMAGE                       COMMAND              CREATED         STATUS         PORTS                                                 NAMES
f0d91de758a6   openshift/hello-openshift   "/hello-openshift"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 8888/tcp   hungry_antonelli
$ service docker restart
Redirecting to /bin/systemctl restart docker.service
$ docker container ls
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS         PORTS                                                 NAMES
f0d91de758a6   openshift/hello-openshift   "/hello-openshift"   22 seconds ago   Up 3 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 8888/tcp   hungry_antonelli
```

### Get Container logs 
```bash
$ docker container ls
CONTAINER ID   IMAGE                       COMMAND              CREATED          STATUS          PORTS                                                 NAMES
f0d91de758a6   openshift/hello-openshift   "/hello-openshift"   19 minutes ago   Up 18 minutes   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 8888/tcp   hungry_antonelli

$ docker container logs -f hungry_antonelli
serving on 8888
serving on 8080
serving on 8888
serving on 8080
```