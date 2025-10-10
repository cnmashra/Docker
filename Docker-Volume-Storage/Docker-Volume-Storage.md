# Docker-Volume-Storage


### Command to list or to view the Docker volume
```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker volume ls
DRIVER    VOLUME NAME
local     0b7d4f354991abfe12d285026a5d1f11ca356aac752457a68a43d98805109060
local     01b5cb022100901dd95b64bec3d64fb3e82f8525d7a83208dcc087ef43325b9a
local     29d2a6acba76e16700968396ee9270b8dc2c9eafcab67bdf87849d6ed1aa3177
local     94a58d60cb6b28ac803a59432acdf870d35abee35f0d059adabd82d3f88de8b2
local     0936d1db4329c5eb38b48782c589e1cd1ff13fd82c496d2972e15f38d46e073c
local     5876b86db849862ca7fdea78414336adc64243973503dfd47ab1f9a0b49ca86c
local     125010fd2e778370ab37da9884ef55817663b88038de498d8e81b7d062a8c516
local     1835845a80bc9b9ce1fc0b19055a22e2336fcf38dce065637310fa257df267bf
local     ffccba4526943f880e94d555b187059dfce91b9984dfcabda45a877e8b3c5176

```

### Command to create the Docker volume manually

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker volume create mysql-data
mysql-data

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker volume ls
DRIVER    VOLUME NAME
local     0b7d4f354991abfe12d285026a5d1f11ca356aac752457a68a43d98805109060
local     01b5cb022100901dd95b64bec3d64fb3e82f8525d7a83208dcc087ef43325b9a
local     29d2a6acba76e16700968396ee9270b8dc2c9eafcab67bdf87849d6ed1aa3177
local     94a58d60cb6b28ac803a59432acdf870d35abee35f0d059adabd82d3f88de8b2
local     0936d1db4329c5eb38b48782c589e1cd1ff13fd82c496d2972e15f38d46e073c
local     5876b86db849862ca7fdea78414336adc64243973503dfd47ab1f9a0b49ca86c
local     125010fd2e778370ab37da9884ef55817663b88038de498d8e81b7d062a8c516
local     1835845a80bc9b9ce1fc0b19055a22e2336fcf38dce065637310fa257df267bf
local     ffccba4526943f880e94d555b187059dfce91b9984dfcabda45a877e8b3c5176
local     mysql-data
```
#### Command to check the mount point created path
```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker inspect mysql-data
[
    {
        "CreatedAt": "2025-10-09T23:46:22Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data",
        "Name": "mysql-data",
        "Options": null,
        "Scope": "local"
    }
]
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker %
```
### command to attch the volume mount while creting the docker (-v means volume)

```
REMOVED TE OLD MYSQL CONTAINER

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED       STATUS       PORTS                                         NAMES
701f2e909c5d   two-tier-backend:latest   "python app.py"          8 hours ago   Up 8 hours   0.0.0.0:5001->5000/tcp, [::]:5001->5000/tcp   sad_heisenberg
99993893f495   mysql                     "docker-entrypoint.s…"   8 hours ago   Up 8 hours   3306/tcp, 33060/tcp                           mysql
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker stop 99993893f495 && docker rm 99993893f495
99993893f495
99993893f495

CREATE MYSQL CONTAINER WITH ATTCHING VOLUME [ -v mysql-data:/var/lib/mysql ]

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker run -d --name mysql --network two-tier -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql
2c8b3a2b123790d832d934a0f670eea41939d538e143110e2492abbbd9d425d4


RESTARTED THE TWO-TIER CONTAINER

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker restart 701f2e909c5d
701f2e909c5d

```

### command to check the Mountpoint volume in the laptop

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker inspect mysql-data
[
    {
        "CreatedAt": "2025-10-09T23:46:22Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data",
        "Name": "mysql-data",
        "Options": null,
        "Scope": "local"
    }
]
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % cd /var/lib/docker/volumes/mysql-data/_data
cd: no such file or directory: /var/lib/docker/volumes/mysql-data/_data
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % sudo su
Password:
sh-3.2# cd /var/lib/docker/volumes/mysql-data/_data
sh: cd: /var/lib/docker/volumes/mysql-data/_data: No such file or directory
sh-3.2#

sh-3.2# exit
exit
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker ps       
CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                                         NAMES
5f2c2668624c   mysql                     "docker-entrypoint.s…"   8 minutes ago   Up 8 minutes   3306/tcp, 33060/tcp                           mysql
701f2e909c5d   two-tier-backend:latest   "python app.py"          8 hours ago     Up 8 minutes   0.0.0.0:5001->5000/tcp, [::]:5001->5000/tcp   sad_heisenberg
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker exec -it 5f2c2668624c bash
bash-5.1# ls /var/lib/docker/volumes/mysql-data/_data
ls: cannot access '/var/lib/docker/volumes/mysql-data/_data': No such file or directory
bash-5.1# sudo su
bash: sudo: command not found
bash-5.1# mysql -u root -proot
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 9.4.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use devops;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> select * from messages;
+----+------------------------------------------------------------------+
| id | message                                                          |
+----+------------------------------------------------------------------+
|  1 | created the mysql with volume mount point storage                |
|  2 | even mysql container removed data will be there in docker volume |
+----+------------------------------------------------------------------+
2 rows in set (0.001 sec)

mysql> exit
Bye
bash-5.1# exit
exit

What's next:
    Try Docker Debug for seamless, persistent debugging tools in any container or image → docker debug 5f2c2668624c
    Learn more at https://docs.docker.com/go/debug-cli/
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker %





```
