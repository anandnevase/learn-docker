## Docker Registory Command


### List Docker Images availabe locally
```bash
[root@10_1_10_6 ~]# docker image ls
REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
fhsinchy/hello-dock         latest    f540930e8157   5 months ago   21.9MB
centos                      latest    300e315adb2f   7 months ago   209MB
openshift/hello-openshift   latest    7af3297a3fb4   3 years ago    6.09MB
```
### Tag docker images locally
```bash
[root@10_1_10_6 ~]# docker image tag openshift/hello-openshift anandnevase/hello-opnenshift
[root@10_1_10_6 ~]# docker image ls
REPOSITORY                     TAG       IMAGE ID       CREATED        SIZE
fhsinchy/hello-dock            latest    f540930e8157   5 months ago   21.9MB
centos                         latest    300e315adb2f   7 months ago   209MB
anandnevase/hello-opnenshift   latest    7af3297a3fb4   3 years ago    6.09MB
openshift/hello-openshift      latest    7af3297a3fb4   3 years ago    6.09MB
```

### Login to DOCKER HUB
```bash
[root@10_1_10_6 ~]# docker login -u anandnevase
Password:
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

### Push Docker Images to docker hub
```bash
[root@10_1_10_6 ~]# docker image push anandnevase/hello-opnenshift
Using default tag: latest
The push refers to repository [docker.io/anandnevase/hello-opnenshift]
da0e4d9121c7: Mounted from openshift/hello-openshift
5f70bf18a086: Mounted from openshift/hello-openshift
latest: digest: sha256:aaea76ff622d2f8bcb32e538e7b3cd0ef6d291953f3e7c9f556c1ba5baf47e2e size: 734
```
### Run Hello Openshift Image    
```bash
$ docker container run --rm -p 8080:8080 anandnevase/hello-opnenshift
```