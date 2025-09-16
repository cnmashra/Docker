## Command to install the Docker
```
sudo apt-get install docker.io
```

## Docker Architecture

### Docker Engine
### Docker Daemon
### Docker CLI
### Docker clinet

### Adding Docker to group for permissions
```
sudo usermod -aG docker $USER
```
Commad to refreshing the after adding new user
```
newgrp docker
```
Command to check the docker images in the host
```
docker images
```
Command to pull/download the docker image
```
docker pull hello-world
```
command to run\install downloaded docker image
```
docker run hello-world
```

Installing the Mysql Docker steps
```
docker pull mysql
docker run -e  MYSQL_ROOT_PASSWORD=root mysql
```


