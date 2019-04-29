# Docker command sheet
Common Docker commands.
## List containers and images
List all images 
```
sudo docker images 
```
List all containers 
```
sudo docker ps -a
```
List runing containers
```
sudo docker ps
```
## Build
```
sudo docker build -f <docker file name>  -t <image selected name:tag> .
```
## Manage containers
Run container (interactive with shell)
```
 docker run -it <image name> bash
```
Run with volume, port, name options 
```
docker run -d \
    --name <container given name> \
    --restart=always \
    -v /tmp:/tmp \
    -p 8080:80 \
    <image name>
```
To run in the background `-d` is used. 


## Stop/start a container
If you already run container, then you stop it. you can start it with.
```
sudo docker stop <container>
sudo docker start <container>
sudo docker -a start <container>
```
If you use start with -a it will return interactive shell. 

# Docker API
You can execute docker commands from a container by binding `/var/run/docker.sock` socket.  
In this example, `manager` container wil send signal to some process in `host` container.  
Run `manager` container and mount `docker.sock` to it.
```
docker run --name manager -it -v /var/run/docker.sock:/var/run/docker.sock imageName bash
```
In side `manager` container install docker python SDK. 
```
pip install docker
```
And then execute this python script
```
import docker
client = docker.from_env()
# run alpine container 
print client.containers.run("alpine", ["echo", "hello", "world"])
# send -HUP singal to proccessName inside containerNme/ID
container = client.containers.get('containerNme/ID')
container.exec_run("pkill -HUP proccessName")
```
More in [here](https://docs.docker.com/develop/sdk/examples/) and [here](https://docker-py.readthedocs.io/en/stable/containers.html)
