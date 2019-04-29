Docker cmd 

Docker HELP!
$ sudo docker --help

Check avialable images:
$ sudo docker images

To remove image
$ sudo docker rmi <imageID>

Run container 
$ sudo docker run -it <imageID> /bin/bash

To check running containers
$ sudo docker ps

To get new shell to the running container
$ sudo docker exec -it <containerID> /bin/bash

To run container in the background
$ sudo docker run -d <imageID>

To get to the background shell of the running container
$ sudo docker attach <containerID>

To stop running container
$ sudo docker stop <containerID>

To remove container 
$ sudo docker rm <containerID>

Build docker image 
 Go to the folder where dockerfile exists
 $ sudo docker build -t <GiveItAName> .

**************************
mount path from the host os to the container
#docker run -it -p 6653:6653 -v /usr/local/lib/python2.7/dist-packages/faucet/:/usr/local/lib/python2.7/dist-packages/faucet/ -v /etc/ryu/faucet/faucet2.yaml:/etc/ryu/faucet/faucet.yaml --name=faucet vuw/faucetimg1 /bin/bash

to run mininet container add --privileged option
#docker run -it --privileged --name=mn ciena/mininet /bin/bash
When you run mn you will find that s1 is down
hence turn it on 
#ifconfig s1 up, then you can access it.

-----------------------
Search for available docker images at
https://hub.docker.com/
e.g.
#docker pull ciena/mininet 
#docker run --privileged ciena/mininet
This mininet image need to be run with --privileged

Docker networking in this link
https://docs.docker.com/engine/tutorials/networkingcontainers/#launch-a-container-on-the-default-network
By default any container will be connected to the deafault bridge called "bridge"
to list them
#docker network ls

To create new bridge
#docker network create -d bridge my_bridge

To connect or disconnect container from your bridge
#docker network connect/disconnect my_bridge <containername/id>

To inspect what containers connected to the bridge
#docker network inspect my_bridge

To run a container in a specific bridge
#docker run -it --name=xyz --net=my_bridge busybox /bin/sh

to inspect container
#docker inspect <coantainerID/name>
--------------

remove all containers
#docker rm $(docker stop $(docker ps -a -q) )

run container with name 
#docker run -it --name=box busybox /bin/sh
----------------
DNS problem 
create 
/etc/docker/daemon.json:

{
    "dns": ["10.0.0.2", "8.8.8.8"]
}
Then restart docker 
sudo service docker restart
