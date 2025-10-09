# DOCKER NETWORK

# Docker Network types

* Host
* Bridge (Default)
* User defined Bridge (custom)
* MACVLAN (docker swarm, cluster related purpose using this network)
* IPVLAN
* Overlay

## Command to check the docker netowrk

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
d9db560c5358   bridge    bridge    local
445ca6bb4485   host      host      local
c34bc0307275   none      null      local

```

## Commadn to create the own docker network

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker network create mynetwork -d bridge
f2287928495a9aff36e435a0fd1f000081d1eaaa4c3921effe4f5d5c311333ce

* -d : it means driver
* bridge : it is the type of docker network name

```
```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker network ls
NETWORK ID     NAME        DRIVER    SCOPE
a5a691160fe8   bridge      bridge    local
445ca6bb4485   host        host      local
f2287928495a   mynetwork   bridge    local
c34bc0307275   none        null      local
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker %
```

