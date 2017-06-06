# docker101

### How to build Docker Image from Dockerfile
## Listing Docker Images


$docker images


## Listing Docker containers

$docker ps 



## How to Build Docker Image


Step-1: Create a Dockerfile(example as shown below):

FROM ubuntu

MAINTAINER "Preet" <preet@gmail.com>



RUN apt-get update

RUN apt-get install screen

Run the below command:

$docker build -t preetk/<imagename> .

This will pick up Dockerfile placed under the current directory.

THis will create a Docker Image.

## How to List the Docker Image?


$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

preetk/image1       latest              34793a04fca9        8 minutes ago       158MB


## How to run a command inside a container without entering into it and it should exit after running the command?

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


As shown above, the docker client ran a container, ran a date command and exited.

## How to Enter into a Container?

Method-1:

$ docker run -it 347 /bin/bash

root@b30778f3fa9e:/#


Once you type exit , it will stop the container.


Method:2:

$ docker run -itd 347 /bin/bash

8f6cc37160d1bb24dd93ab430ce772386cc7c21d5386b23a71ba1af55fab3b70

[node1] (local) root@10.0.39.3 ~

$

-d option runs the container in the background.

