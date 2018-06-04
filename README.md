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
