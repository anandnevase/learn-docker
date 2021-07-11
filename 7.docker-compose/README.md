## Docker Compose

### Install docker Compose
```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

$ docker-compose --version
docker-compose version 1.26.2, build 1110ad01
```

### Build Multicontainer from docker-compose
```bash
$ docker-compose build
database uses an image, skipping
Building web
Step 1/11 : FROM python:3.9-rc-buster
 ---> 2e0edf7d3a8a
Step 2/11 : RUN apt-get update && apt-get install -y docker.io

```

### docker-compose Image
```bash
$ docker-compose images
          Container                  Repository        Tag       Image Id       Size  
--------------------------------------------------------------------------------------
7001788f31a9_docker_database_1   mysql/mysql-server   5.7      2a6c84ecfcb2   333.9 MB
docker_database_1                mysql/mysql-server   5.7      2a6c84ecfcb2   333.9 MB
docker_web_1                     <none>               <none>   d986d824dae4   953 MB
```

### Stop containers
```bash
$ docker-compose stop
Stopping docker_web_1      ... done
Stopping docker_database_1 ... done

```

### Start only one container
```bash
$ docker-compose run web
Starting 7001788f31a9_docker_database_1 ... done
 * Serving Flask app "app.py" (lazy loading)
 * Environment: development
 * Debug mode: on
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 116-917-688
```

### Start all containers
```bash
$ docker-compose up
Creating docker_database_1 ... done
Creating docker_web_1      ... done
Attaching to docker_database_1, docker_web_1
```

### Check all containers
```bash
$ docker-compose ps
      Name                 Command             State               Ports         
---------------------------------------------------------------------------------
docker_database_1   /entrypoint.sh mysqld   Up (healthy)   3306/tcp, 33060/tcp   
docker_web_1        flask run               Up             0.0.0.0:5000->5000/tcp
 
$ docker-compose ps
      Name                 Command          State    Ports
----------------------------------------------------------
docker_database_1   /entrypoint.sh mysqld   Exit 0        
docker_web_1        flask run               Exit 0   
```

### Remove all containers
```bash
$ docker-compose down
Removing docker_web_1      ... done
Removing docker_database_1 ... done
Removing network docker_default
(django-tuts) Venkateshs-MacBook-Air:Docker venkateshachintalwar$ docker-compose images
Container   Repository   Tag   Image Id   Size
----------------------------------------------
(django-tuts) Venkateshs-MacBook-Air:Docker venkateshachintalwar$ docker-compose ps
Name   Command   State   Ports
------------------------------
```