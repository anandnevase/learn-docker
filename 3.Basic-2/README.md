## Basic Docker Command

### 1. Volume Mounting on Docker Container to persist data

```bash
   docker run --name <container-name> -v <host-vol-path>:<container-vol-path> -p <host-port>:<container-port> <image-name>
```  
Example
```bash
# create Volume mount to access index.html from httpd container
$ docker run --name httpd -d -p 8080:80 

# Test application using. 
# You can see "its works" or "nginx"  output
$ curl <host-ip>:8080

# delete container
$ docker rm -f httpd

# create tmp app folder
$ mkdir -p /tmp/app

# create index.html file
$ echo "Hello World" > /tmp/app/index.html

# create Volume mount to access index.html from httpd container
$ docker run --name httpd  --rm -v /tmp/app:/usr/local/apache2/htdocs -d -p 8080:80 

# Test application using. 
# You can see Hello World output
$ curl <host-ip>:8080

# restart app and check output
$ docker restart httpd

```

### 2. How to Commit/create image and push to docker repo (DOKER HUB)
```bash
   docker commit <container-name/id> -t <new-image-name>
         OR
   docker commit <container-name/id> -t <new-image-name>:<tag>
```  

Example
```bash
# commit image and save with name "myimage"
$ docker commit   myimage
sha256:9a2bbb16a1778c7728102f582a4255a238577627af1c9c101e95a821d6dd692f

# login to docker repo (default: DOCKER-HUB)
$ docker login -u anandnevase
Password:
WARNING! Your password will be stored unencrypted in /home/nevase_anand/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

# docker tag image based on repo 

$ docker tag myimage anandnevase/demo-image
$ docker images
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
anandnevase/demo-image   latest              9a2bbb16a177        8 minutes ago       107MB
myimage                  latest              9a2bbb16a177        8 minutes ago       107MB
httpd                    latest              ccbcea8a6757        2 days ago          166MB
httpd                    alpine              eee6a6a3a3c9        6 weeks ago         107MB

$ docker push anandnevase/demo-image
The push refers to repository [docker.io/anandnevase/demo-image]
56b126295e2d: Layer already exists
75330f1d6f1c: Layer already exists
0d648f7641c2: Layer already exists
ee4c544f5273: Layer already exists
c1a19e8cc45c: Layer already exists
3e207b409db3: Layer already exists
latest: digest: sha256:6c1e7580ae122878ae4a0e5a529086d430ea046a8a09ba26747d2a6522805c67 size: 1569n
```