# Getting Started with Docker on Ubuntu

### My system specs
Ubuntu 18.04 Bionic

## Install docker

1. Remove older versions if installed

    ```
    $ sudo apt-get remove docker docker-engine docker.io
    ```

2. Add docker APT repository

    ```
    $ sudo apt-get update
    
    $ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

    # Add APT key
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    # Verify key
    $ sudo apt-key fingerprint 0EBFCD88

    # Add repo
    $ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

   $ sudo apt-get update
    ```

3. Install docker

    ```
    $ sudo apt-get install docker-ce
    ```

4. Verify docker installation

    ```
    $ sudo docker run hello-world

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

    To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

    For more examples and ideas, visit:
    https://docs.docker.com/engine/userguide/
    ```

## List running containers

```
$ sudo docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

## List all containers and history

```
$ sudo docker container ls --all
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
26ac3dc493a6        hello-world         "/hello"            5 minutes ago       Exited (0) 5 minutes ago                       inspiring_agnesi
3553645d7027        ubuntu              "bash"              4 months ago        Exited (0) 4 months ago                        modest_fermat
8763e0c558b0        ubuntu              "bash -d"           4 months ago        Exited (2) 4 months ago                        boring_saha
f5c53ba715e3        ubuntu              "bash"              4 months ago        Exited (0) 4 months ago                        loving_darwin
0135e1550085        ubuntu              "bash"              4 months ago        Exited (0) 4 months ago                        determined_johnson
a1875f3c53c5        hello-world         "/hello"            4 months ago        Exited (0) 4 months ago                        elegant_edison
```

## Docker version

```
$ sudo docker -v
Docker version 18.09.0, build 4d60db4

$ sudo docker --version
Docker version 18.09.0, build 4d60db4
```

## Detailed information

```
$ sudo docker info

Containers: 6
Running: 0
Paused: 0
Stopped: 6
Images: 2
Server Version: 18.09.0
Storage Driver: overlay2
Backing Filesystem: xfs
Supports d_type: true
Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
Volume: local
Network: bridge host macvlan null overlay
Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: c4446665cb9c30056f4998ed953e6d4ff22c7c39
runc version: 4fc53a81fb7c994640722ac585fa9ca548971871
init version: fec3683
Security Options:
apparmor
seccomp
Profile: default
Kernel Version: 4.15.0-15-generic
Operating System: Ubuntu Bionic Beaver (development branch)
OSType: linux
Architecture: x86_64
CPUs: 4
Total Memory: 15.55GiB
Name: HimanshuG
ID: WXFK:F2FK:6FFQ:B4Q3:HV44:GZ3L:5GQT:ZKNA:NIGL:BJPZ:RQWY:LNC4
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
Labels:
Experimental: false
Insecure Registries:
127.0.0.0/8
Live Restore Enabled: false
Product License: Community Engine

WARNING: No swap limit support

```

## List docker images available

```
$ sudo docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              2cb0d9787c4d        4 months ago        1.85kB
ubuntu              latest              113a43faa138        5 months ago        81.2MB
```

## Fetch remote image and run it

In order to fetch an image from docker hub (repository of open source docker images) and run container out of it

```
$ sudo docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

This will first look for the image on local system and if it is not found, then fetch it from docker hub and start the container

```
Unable to find image 'sonarqube:latest' locally
latest: Pulling from library/sonarqube
bc9ab73e5b14: Pull complete 
193a6306c92a: Pull complete 
e5c3f8c317dc: Pull complete 
a587a86c9dcb: Pull complete 
a4c7ee7ef122: Pull complete 
a7c0dad691e9: Pull complete 
367a6a68b113: Pull complete 
60c0e52d1ec2: Pull complete 
c9d22bc43935: Pull complete 
884af0bfbb9a: Pull complete 
35a8cd0c916a: Pull complete 
9f9ecbe7a343: Pull complete 
af800bded4f3: Pull complete 
Digest: sha256:cc57b262ee9e7145456dee8c7ae24622c82b22cabeaac4651e7dd642da806f2e
Status: Downloaded newer image for sonarqube:latest
91cc58ad0c2c7c24e7f6d530f1dbf507b1bbfbee6e92cac39a03f8ef4ddee7af
```

## Login to container

```
$ sudo docker exec -it sonarqube /bin/bash

root@91cc58ad0c2c:/opt/sonarqube#
```

Only run command and exit

```
$ sudo docker exec -it sonarqube hostname
91cc58ad0c2c
```
