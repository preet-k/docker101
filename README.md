
<h1> How to build Docker Image from Dockerfile</h1>

## Listing Docker Imagess


```$docker images
```

## Listing Docker containers

```
$docker ps 
```


## How to Build Docker Image


Step-1: Create a Dockerfile(example as shown below):

```FROM ubuntu

MAINTAINER "Preet" <preet@gmail.com>



RUN apt-get update

RUN apt-get install screen

```

Run the below command:

```
$docker build -t preetk/<imagename> .
```

This will pick up Dockerfile placed under the current directory.

THis will create a Docker Image.

## How to List the Docker Image?


```
$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

preetk/image1       latest              34793a04fca9        8 minutes ago       158MB
```

## How to run a command inside a container without entering into it and it should exit after running the command?

```
$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

preetk/image1       latest              34793a04fca9        11 minutes ago      158MB

[node1] (local) root@10.0.39.3 ~
$ docker run 347 date

Tue Jun  6 09:31:05 UTC 2017


[node1] (local) root@10.0.39.3 ~
$ docker ps

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS
     PORTS               NAMES

[node1] (local) root@10.0.39.3 ~
$
```

As shown above, the docker client ran a container, ran a date command and exited.

## How to Enter into a Container?

<b>Method-1:</b>

```
$ docker run -it 347 /bin/bash
root@b30778f3fa9e:/#
```

Once you type exit , it will stop the container.


<b>Method:2:</b>

```
$ docker run -itd 347 /bin/bash

8f6cc37160d1bb24dd93ab430ce772386cc7c21d5386b23a71ba1af55fab3b70

[node1] (local) root@10.0.39.3 ~

$
```

-d refers to daemon which runs the container in the background.


<b> Method:3</b>

```
$docker run -itd 347 /bin/bash
$docker attach <containerid>

```
## How to save using commit?


Step-1: Press Ctrl+P+Q to come out of container without stopping it

Step-2: RUn the below command to commit the changes:

```
$docker commit -m " Comment" <container-id> preetk/newimagename
```

This is the first time we are creating Image out of running container.

Please note that the container will be in running state.

## Concept of Ports & Networking

You can run multiple Web Server inside the same host in the form of container. So it means you can have multiple containers running under port 80. But when you try to expose it to your Docker host then it should have different ports.

For Example:

Container C1 runs Web Server at port 80 
Container C2 runs Web Server at Port 80

If Container C1 port gets exposed to Docker Host at Port 80, then Container C2 port shouldnt be exposed at the right port. It
could either be at port 81 or port 82.

## Sample of Dockerfile for Apache installed on Ubuntu 
```
FROM ubuntu

MAINTAINER "Preet" preet@gmail.com

RUN apt-get update

RUN apt-get -y install apache2 

RUN service apache2 start 

EXPOSE 80

EXPOSE 443 

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```







