
<h1> How to build Docker Image from Dockerfile</h1>

## Listing Docker Images


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

## Volume

```

docker run -itd -p 80:80 -p 443:443 preetk/ubuntuwithapache
    2  clear
    3  vi index.html
    4  docker run -itd preetk/ubuntuwithapache
    5  docker ps
    6  docker attach
    7  docker run -itd preetk/ubuntuwithapache /bin/bash
    8  docker attach 21cfe009abf3
    9  docker run -itd preetk/ubuntuwithapache /bin/bash
   10  docker ps
   11  docker run -it preetk/ubuntuwithapache /bin/bash
   12  clear
   13  pwd
   14  docker stop $(docker ps -a -q)
   15  clear
   16  pwd
   17  cat index.html
   18  clear
   19  docker run -d -v /root/index.html:/var/www/html/ -p 80:80 -p 443:443 preetk/ubuntuwithap
ache
   20  docker run -d -v /root/index.html:/var/www/html/index.html -p 80:80 -p 443:443 preetk/ub
untuwithapache
   21  docker ps
clear
   23  docker ps
   24  docker exec -it 2b7 echo "Hiiii" >> /var/www/html/index.html
   25  docker exec -it 2b7 /bin/echo "Hiiii" >> /var/www/html/index.html
   26  docker exec -it 2b7 /bin/bash
   27  docker exec -it 2b7 echo hi
   28  clear
   29  docker ocpy
   30  docker copy
   31  docker cp
   32  clear
   33  git clone https://github.com/preetk/docker101
   34  git clone https://github.com/preetk/docker101
   35  git clone https://github.com/preet-k/docker101
   36  cd docker101
   37  clear
   38  ls
   39  vi Dockerfile
   40  exitr
   41  exit
   42  mkdir mydir
   43  ls
   cp index.html mydir
   45  git clone https://www.github.com/preet-k/docker101/Chapter-1
   46  git clone https://www.github.com/preet-k/docker101
   47  git clone https://www.github.com/preet-k/docker101/
   48  git clone https://github.com/preet-k/docker101/
   49  cd docker101
   50  ls Chapter-1
   51  cd Chapter-1/
   52  ls
   53  vi Dockerfile-ubuntuwithapache
   54  docker build -t preetk/volume .
   55  cd ..
   56  cd ..
   57  vi Dockerfile
   58  pwd
   59  ls
   60  cd docker101
   61  cd Chapter-1
   62  ls
   63  vi Dockerfile-ubuntuwithapache
   64  docker build -t preetk/volume .
   65  ls
   pwd
   67  clear
   68  ls
   69  ls
   70  cd
   71  ls
   72  cd -
   73  clear
   74  vi Dockerfile-ubuntuwithapache
   75  clear
   76  docker build -t preetk/volume .
   77  ls
   78  cd
   79  ls
   80  clear
   81  pwd
   82  ls
   83  cd mydir/
   84  ls
   85  cd ..
   86  ls
   87  tar cvf mydir.tar.gz mydir/
   88  clear
   ls
   90  pwd
   91  cd docker101/Chapter-1/
   92  clear
   93  ls
   94  vi Dockerfile-ubuntuwithapache
   95  clear
   96  docker build -t preetk/volume .
   97  docker run -itd f3 /bin/bash
   98  docker ps
   99  clear
  100  docker ps
  101  docker stop 2b
  102  docker stop 1e
  103  clear
  104  docker images
  105  docker run -dit f37 /bin/bash
  106  docker ps
  107  docker attach 032
  108  docker ps
  109  docker images
  110  ls
  111  vi Dockerfile-ubuntuwithapache
  112  clear
  ls
  114  cp -rf /root/mydir.tar.gz .
  115  ls
  116  vi Dockerfile
  117  clera
  118  clear vi Dockerfileclear
  119  vi Dockerfile-ubuntuwithapache
  120  clear
  121  docker build -t preetk/vol1 .
  122  clear
  123  ls
  124  mkdir mydir
  125  cp mydir.tar.gz mydir/
  126  clear
  127  ls
  128  vi Dockerfile
  129  mv Dockerfile-ubuntuwithapache Dockeerfile
  130  mv Dockerfile-ubuntuwithapache Dockrfile
  131  mv Dockeerfile Dockerfile
  132  clear
  133  ls
  134  cat Dockerfile
  135  clear
  136  vi Dockerfile
  ls
  138  cd mydir/
  139  ls
  140  cd ..
  141  rm -fr mydir.tar.gz
  142  clear
  143  ls
  144  docker build -t preetk/vol2 .
  145  clear
  146  docker history
  147  history
  148  top
  149  history
[node1] (local) root@10.0.51.3 ~/docker101/Chapter-1
$ B

```
### To mention the dockerfile for building.
```
 docker build -t preetk/web2 -f /root/docker101/Chapter-1/Dockerfile-ubuntuwithapache .
 ```
 ### To run python and know version directly.
 ```
 docker run python python -V
 ```
 ### Using Compose
 ```
 vi docker-compose.yml
 > docker-compose.yml
 docker-compose up -d
``` 
 ### History
 clear                                            
 vi docker-compose.yml                                                                                           vi   docker-compose.yml                                                                        5  vi docker-compose.yml                                                                        6  vi rm docker-compose.yml                                                                     7  clear                                                                                        8  clear                                                                                        9  vi docker-compose.yml                                                                       10  vi docker-compose.yml                                                                       11  > docker-compose.yml                                                                        12  vi docker-compose.yml                                                                       13  clear                                                                                       14  cat docker-compose.yml                                                                      15  clear                                                                                       16  vi docker-compose.yml
 
 


### Today
git pull CentOS/CentOS-Dockerfiles
    2  git clone CentOS/CentOS-Dockerfiles
    3  git clone CentOS/CentOS-Dockerfiles/httpd/centos7/
    4  git clone http://github.com/CentOS/CentOS-Dockerfiles/httpd/centos7/
    5  git clone https://github.com/CentOS-Dockerfiles/httpd/centos7/
    6  git clone https://github.com/CentOS-Dockerfiles/httpd/centos7/Dockerfile
    7  git clone https://github.com/CentOS/CentOS-Dockerfiles
    8  ls
    9  cd CentOS-Dockerfiles/
   10  ls
   11  cd httpd
   12  ls
   cd centos7
   14  ls
   15  vi Dockerfile
   16  docker build -t preetk/centwithapache .
   17  docker run -itd -p 80:80 preetk/centwithapache
   18  docker ps
   19  vi Dockerfile
   20  docker run -itd -p 80:80 preetk/centwithapache /bin/sh
   21  docker run -itd -p 81:80 preetk/centwithapache /bin/sh
   22  ls
   23  docker attach d13a0b280f521c6b0eb3dcef3ec79452db5a66a8ce046569f2949
   24  vi index.html
   25  docker run -itd -v root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ wq-p
 81:80 preetk/centwithapache /bin/sh
   26  docker run -itd -v root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ wq-p
 81:80 preetk/centwithapache /bin/sh
   27  docker run -itd -v root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ -p 8
1:80 preetk/centwithapache /bin/sh
   28  pwd
   29  docker run -itd -v /root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ -p
81:80 preetk/centwithapache /bin/sh
   30  docker run -itd -v /root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ -p
82:80 preetk/centwithapache /bin/sh
31  docker run -itd -v /root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ -p
82:80 preetk/centwithapache
   32  docker ps
   33  docker rm $(ps -a)
   34  docker run -itd -v /root/CentOS-Dockerfiles/httpd/centos7/index.html:/var/www/html/ -p
82:80 preetk/centwithapache /bin/bash
   35  docker ps
   36  docker rm d13a0b280f52
   37  docker stop d13a0b280f52
   38  docker stop 49a75af94c8d
   39  docker ps
   40  history
