## Multistage Dockerfile

### Build custom-nginx from multistage dockerfile
```bash
$ docker image build -t custom-nginx .
Sending build context to Docker daemon  95.75MB
Step 1/4 : FROM nginx:alpine
alpine: Pulling from library/nginx
5843afab3874: Pull complete
0dc18a5274f2: Pull complete
48a0ee941dcd: Pull complete
2446243a1a3f: Pull complete
cbf0756b41fb: Pull complete
c72750a979b9: Pull complete
Digest: sha256:91528597e842ab1b3b25567191fa7d4e211cb3cc332071fa031cfed2b5892f9e
Status: Downloaded newer image for nginx:alpine
 ---> b9e2356ea1be
Step 2/4 : LABEL maintainer="anandnevase"
 ---> Running in 5736cfacddb9
Removing intermediate container 5736cfacddb9
 ---> 2cd63199da7f
Step 3/4 : COPY index.html /usr/share/nginx/html/
 ---> c6a397832c96
Step 4/4 : ENTRYPOINT ["nginx", "-g", "daemon off;"]
 ---> Running in 6656fd6bd5dd
Removing intermediate container 6656fd6bd5dd
 ---> 93fe32fbc71c
Successfully built 93fe32fbc71c
Successfully tagged custom-nginx:latest
```

### checkk custom-nginx image
```bash
$ docker image ls
REPOSITORY                     TAG       IMAGE ID       CREATED          SIZE
custom-nginx                       latest    93fe32fbc71c   39 seconds ago   22.8MB
nginx                          alpine    b9e2356ea1be   4 days ago       22.8MB
```
### Run container custom-nginx
```bash
$ docker container run -d -p 80:80 --restart=always custom-nginx
14aea4c847be41ed4c8b4a816eba45b8f24af187632c7002efb03eaece10b6d5
$ curl http://localhost:80
Welcome to Dockerlabs!!
```