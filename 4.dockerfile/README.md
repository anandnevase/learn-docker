## Dockerfile

### Build my-nginx from dockerfile
```bash
$ docker image build -t my-nginx .
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
Successfully tagged my-nginx:latest
```

### checkk my-nginx image
```bash
$ docker image ls
REPOSITORY                     TAG       IMAGE ID       CREATED          SIZE
my-nginx                       latest    93fe32fbc71c   39 seconds ago   22.8MB
nginx                          alpine    b9e2356ea1be   4 days ago       22.8MB
```
### Run container my-nginx
```bash
$ docker container run -d -p 80:80 --restart=always my-nginx
14aea4c847be41ed4c8b4a816eba45b8f24af187632c7002efb03eaece10b6d5
$ curl http://localhost:80
Welcome to Dockerlabs!!
```

### Image history
```bash
$ docker image ls
REPOSITORY                     TAG       IMAGE ID       CREATED         SIZE
my-nginx                       latest    93fe32fbc71c   5 minutes ago   22.8MB
nginx                          alpine    b9e2356ea1be   4 days ago      22.8MB
fhsinchy/hello-dock            latest    f540930e8157   5 months ago    21.9MB
centos                         latest    300e315adb2f   7 months ago    209MB
openshift/hello-openshift      latest    7af3297a3fb4   3 years ago     6.09MB
anandnevase/hello-opnenshift   latest    7af3297a3fb4   3 years ago     6.09MB
$ docker image history my-nginx
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
93fe32fbc71c   5 minutes ago   /bin/sh -c #(nop)  ENTRYPOINT ["nginx" "-g" …   0B
c6a397832c96   5 minutes ago   /bin/sh -c #(nop) COPY file:1d2ed5994589d087…   5B
2cd63199da7f   5 minutes ago   /bin/sh -c #(nop)  LABEL maintainer=Collabnix   0B
b9e2356ea1be   4 days ago      /bin/sh -c #(nop)  CMD ["nginx" "-g" "daemon…   0B
<missing>      4 days ago      /bin/sh -c #(nop)  STOPSIGNAL SIGQUIT           0B
<missing>      4 days ago      /bin/sh -c #(nop)  EXPOSE 80                    0B
<missing>      4 days ago      /bin/sh -c #(nop)  ENTRYPOINT ["/docker-entr…   0B
<missing>      4 days ago      /bin/sh -c #(nop) COPY file:09a214a3e07c919a…   4.61kB
<missing>      4 days ago      /bin/sh -c #(nop) COPY file:0fd5fca330dcd6a7…   1.04kB
<missing>      4 days ago      /bin/sh -c #(nop) COPY file:0b866ff3fc1ef5b0…   1.96kB
<missing>      4 days ago      /bin/sh -c #(nop) COPY file:65504f71f5855ca0…   1.2kB
<missing>      4 days ago      /bin/sh -c set -x     && addgroup -g 101 -S …   17.2MB
<missing>      4 days ago      /bin/sh -c #(nop)  ENV PKG_RELEASE=1            0B
<missing>      4 days ago      /bin/sh -c #(nop)  ENV NJS_VERSION=0.6.1        0B
<missing>      4 days ago      /bin/sh -c #(nop)  ENV NGINX_VERSION=1.21.1     0B
<missing>      4 days ago      /bin/sh -c #(nop)  LABEL maintainer=NGINX Do…   0B
<missing>      3 weeks ago     /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
<missing>      3 weeks ago     /bin/sh -c #(nop) ADD file:f278386b0cef68136…   5.6MB
```
