TM: 100.98.26.33
SUT: 100.98.26.38

All Docker containers stopped on both TM and SUT

============================

Phase: 1 - Run the below command on SUT and TM both

1. Stop HTTPD 

$service httpd stop

2. Stop Firewall

$service firewalld stop

=============================================

Phase:2 - Pull the preetk/redhatcert image on both the SUT and TM

$docker pull preetk/redhatcert

================================================

Phase:3 - Run the below command on both SUT and TM and keep it running.

$docker run --privileged --net=host -ti -e container=docker -v /sys/fs/cgroup:/sys/fs/cgroup preetk/rhcertification /usr/sbin/init

======================================

Phase:4 - Run these commands on both the SUT and TM

[root@testmanager ~]# docker exec -it e173 service httpd start
Redirecting to /bin/systemctl start  httpd.service
[root@testmanager ~]# docker exec -it e173 service firewalld stop
Redirecting to /bin/systemctl stop  firewalld.service
[root@testmanager ~]#

====================================================

Phase:5 - Start the TM Server

$docker exec -it <container-id> rhcertd start

Start the SUT Server:

$docker exec -it <container-id> rhcert-cli register --server <TM IP>


==================================================
