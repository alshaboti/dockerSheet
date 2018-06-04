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
sudo docker build -f Dockerfile.faucet.pi -t <image selected name:tag> .
```

## Manage containers
Run container (interactive with shell)
```
 docker run -it <image name> bash
```
