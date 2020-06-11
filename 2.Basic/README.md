## Basic Docker Command

### 1. Starting Web container With PORT mapping

```bash
   docker run --name <container-name> -p <host-port>:<container-port> <image-name>
```  
Example
```bash
$ docker run -p 8080:8080  openshift/hello-openshift
serving on 8888
serving on 8080
Servicing request.

# Once you close (CLTR+C) container will be stopped 
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
$ docker ps -a
CONTAINER ID        IMAGE                       COMMAND              CREATED              STATUS                      PORTS               NAMES
ba14dcec438a        openshift/hello-openshift   "/hello-openshift"   About a minute ago   Exited (2) 24 seconds ago                       keen_rubin

```
### 2. Starting Web container With PORT mapping in Detached (-d) Mode
```bash
   docker run --name <container-name> -d -p <host-port>:<container-port> <image-name>
```  

Example
```bash
$ docker run -d -p 8080:8080  openshift/hello-openshift
d8a646fdd504268dc62dd5839ee4099ad35bb3948da9a8b4a4c4b88194ef43bd

$ docker ps
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS              PORTS                              NAMES
d8a646fdd504        openshift/hello-openshift   "/hello-openshift"   8 seconds ago       Up 7 seconds        0.0.0.0:8080->8080/tcp, 8888/tcp   musing_galois
```
### 3. If we start new web container With same PORT, You will see 'port is already allocated' ERROR
```
# You will observe that,  port is already allocated error we get
$ docker run -d -p 8080:8080  openshift/hello-openshift
9e0f6d6d73ce5680a3828817f46f0d7bb7d50543a0ec39343c3dfe60c7e920a0
docker: Error response from daemon: driver failed programming external connectivity on endpoint silly_shirley (2b71370acbf69874c82709cce7d1d459d18a2fbfc2fc21f1f28ca11049eaedd9): Bind for 0.0.0.0:8080 failed: port is already allocated.

# starting container with 9090 port
$ docker run -d -p 9090:8080  openshift/hello-openshift
9f4c26ebe66025324b03b232b2d84c7776c3e1323c3dc860e3adb9172d0c213e

$ docker ps
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS              PORTS                              NAMES
9f4c26ebe660        openshift/hello-openshift   "/hello-openshift"   3 seconds ago       Up 2 seconds        8888/tcp, 0.0.0.0:9090->8080/tcp   nifty_banzai
d8a646fdd504        openshift/hello-openshift   "/hello-openshift"   2 minutes ago       Up 2 minutes        0.0.0.0:8080->8080/tcp, 8888/tcp   musing_galois
$
ba14dcec438a        openshift/hello-openshift   "/hello-openshift"   7 minutes ago       Exited (2) 6 minutes ago                                       keen_rubin
3a0738ef08c9        openshift/hello-openshift   "/hello-openshift"   10 minutes ago      Exited (2) 8 minutes ago                                       brave_wozniak
```
### 4. Stopped Running container


```bash   
   docker stop <container-name> or <container-id> 
```  
Example
```bash

$ docker stop keen_rubin
nifty_banzai

$ docker ps -a
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS                     PORTS                              NAMES
ba14dcec438a        openshift/hello-openshift   "/hello-openshift"   1 minutes ago       Exited (2) 6 minutes ago                                      keen_rubin
3a0738ef08c9        openshift/hello-openshift   "/hello-openshift"   10 minutes ago      Exited (2) 9 minutes ago                                      brave_wozniak
```

### 5. Starting  container


```bash   
   docker start <container-name> or <container-id> 
```  
Example
```bash
$ docker start keen_rubin
nifty_banzai

$ docker ps -a
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS                     PORTS                              NAMES
9f4c26ebe660        openshift/hello-openshift   "/hello-openshift"   2 minutes ago       Up 8 seconds               8888/tcp, 0.0.0.0:9090->8080/tcp   keen_rubin
```

### 6. Restarting  container


```bash   
   docker restart <container-name> or <container-id> 
```  
Example
```bash
# restarting using container-id
$ docker restart 9f4c26ebe660
9f4c26ebe660

$ docker ps 
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS              PORTS                              NAMES
9f4c26ebe660        openshift/hello-openshift   "/hello-openshift"   4 minutes ago       Up 5 seconds        8888/tcp, 0.0.0.0:9090->8080/tcp   keen_rubin
```
### 7. Remove Container


```bash   
   docker search <image-name-to-search>
```  
Example
```bash

$ docker ps 
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS              PORTS                              NAMES
9f4c26ebe660        openshift/hello-openshift   "/hello-openshift"   4 minutes ago       Up 5 seconds        8888/tcp, 0.0.0.0:9090->8080/tcp   keen_rubin

# Removing container using image id. 

$ docker rm 9f4c26ebe660
9f4c26ebe660

# if container is running, and you forcefully want to rm used -f option
$ docker rm -f 9f4c26ebe660
9f4c26ebe660
```

### 8. Search Image


```bash   
   docker search <image-name-to-search>
```  
Example
```bash
$ docker search http 
```

### 9. By default Docker container will stop if Docker-Engine(daemon)/machine restarted
```bash
$ docker ps
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS              PORTS                              NAMES
9feb55fa3484        httpd                       "httpd-foreground"   51 seconds ago      Up 49 seconds       0.0.0.0:9090->80/tcp               httpd
d8a646fdd504        openshift/hello-openshift   "/hello-openshift"   21 minutes ago      Up 21 minutes       0.0.0.0:8080->8080/tcp, 8888/tcp   musing_galois

$ docker exec -i -t httpd sh
# hostname
9feb55fa3484

$ service docker status
Docker is running.

$ service docker stop
Docker must be run as root ... failed!

$ sudo service docker stop
Stopping Docker: docker.

$ service docker status
Docker is not running ... failed!

$ docker images
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

$ sudo service docker start
Starting Docker: docker.

$ service docker status
Docker is running.

$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

$ docker ps  -a
CONTAINER ID        IMAGE                       COMMAND              CREATED             STATUS                      PORTS               NAMES
9e0f6d6d73ce        openshift/hello-openshift   "/hello-openshift"   28 minutes ago      Created                                         silly_shirley
d8a646fdd504        openshift/hello-openshift   "/hello-openshift"   29 minutes ago      Exited (2) 3 minutes ago                        musing_galois
ba14dcec438a        openshift/hello-openshift   "/hello-openshift"   31 minutes ago      Exited (2) 31 minutes ago                       keen_rubin
```

### 10. Configuring Docker container to restart even if Docker-Engine(daemon)/machine is rebooted, using --restart=always option
```bash
$ docker run -it --name httpd-restart --restart always -d -p 9090:80 httpd
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