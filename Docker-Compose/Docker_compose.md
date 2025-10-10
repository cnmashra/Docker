# DOCKER COMPOSE

Docker compose: We can create the multiple docker containner in the same file

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % cat docker-compose.yml
version: "3.8"

services:
  mysql:
    container_name: mysql
    image: mysql
    environment: 
      MYSQL_DATABASE: "devops"
      MYSQL_ROOT_PASSWORD: "root"
    ports: 
      - "3306:3306"
    volumes:
      - mysql-data:/var/lib/mysql
    networks:
      - two-tier
    restart: always
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-uroot", "-proot"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 60s 

  flask:
    build:
      context: .
    container_name: two-tier-backend
    ports:
      - "5001:5000"
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: root
      MYSQL_DB: devops
    networks: 
      - two-tier
    depends_on:
      - mysql
    restart: always
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:5001/health || exit 1"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 60s

volumes:
  mysql-data:

networks:
  two-tier:


raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker compose up -d
WARN[0000] /Users/raghavendracn/Documents/Docker/two-tier-flask-app/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 2/2
 ✔ Container mysql             Started                                                                                                    0.1s 
 ✔ Container two-tier-backend  Started                                                                                                    0.1s 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 


raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker ps
CONTAINER ID   IMAGE                      COMMAND                  CREATED         STATUS                     PORTS                                         NAMES
19ecf22d03e2   two-tier-flask-app-flask   "python app.py"          3 minutes ago   Up 2 minutes (unhealthy)   0.0.0.0:5001->5000/tcp, [::]:5001->5000/tcp   two-tier-backend
d1f0cf8338c9   mysql                      "docker-entrypoint.s…"   3 minutes ago   Up 2 minutes (healthy)     0.0.0.0:3306->3306/tcp, [::]:3306->3306/tcp   mysql
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker exec -it d1f0cf8338c9 bash
bash-5.1# mysql -u root -proot
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 35
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
+----+----------------------------+
| id | message                    |
+----+----------------------------+
|  1 | Created the docker compose |
|  2 | succesfully                |
|  3 | using command              |
|  4 | docker compose up -d       |
+----+----------------------------+
4 rows in set (0.001 sec)

mysql> exit
Bye
bash-5.1# exit
exit

What's next:
    Try Docker Debug for seamless, persistent debugging tools in any container or image → docker debug d1f0cf8338c9
    Learn more at https://docs.docker.com/go/debug-cli/
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker compose down
WARN[0000] /Users/raghavendracn/Documents/Docker/two-tier-flask-app/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 3/3
 ✔ Container two-tier-backend           Removed                                                                                           0.2s 
 ✔ Container mysql                      Removed                                                                                           1.3s 
 ✔ Network two-tier-flask-app_two-tier  Removed                                                                                           0.2s 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app %


```

#### another command to create the container using docker compose

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker compose up -d build
WARN[0000] /Users/raghavendracn/Documents/Docker/two-tier-flask-app/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
no such service: build
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker compose up -d --build
WARN[0000] /Users/raghavendracn/Documents/Docker/two-tier-flask-app/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 11/11
 ✔ mysql Pulled                                                                                                                          70.3s 
   ✔ ecb83b09a418 Pull complete                                                                                                          26.5s 
   ✔ 91beec75ea95 Pull complete                                                                                                          26.5s 
   ✔ 113f24e83af6 Pull complete                                                                                                          26.5s 
   ✔ 20e973ad942c Pull complete                                                                                                          26.6s 
   ✔ 49bbd3f4ed8c Pull complete                                                                                                          26.6s 
   ✔ ecd21296720f Pull complete                                                                                                          26.7s 
   ✔ fbda0e12a0b6 Pull complete                                                                                                          33.5s 
   ✔ 42a31c1f092c Pull complete                                                                                                          33.5s 
   ✔ 716452459d78 Pull complete                                                                                                          66.4s 
   ✔ ae25a9a46a8f Pull complete                                                                                                          66.4s 
[+] Building 2.3s (15/15) FINISHED                                                                                                             
 => [internal] load local bake definitions                                                                                                0.0s
 => => reading from stdin 583B                                                                                                            0.0s
 => [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 669B                                                                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.9-slim                                                                        2.1s
 => [auth] library/python:pull token for registry-1.docker.io                                                                             0.0s
 => [internal] load .dockerignore                                                                                                         0.0s
 => => transferring context: 2B                                                                                                           0.0s
 => [1/7] FROM docker.io/library/python:3.9-slim@sha256:0bc9ce8b3c40e7892a575cd44ea16c673ac497c6eb0e6a51aa40ee3d85033bcb                  0.0s
 => => resolve docker.io/library/python:3.9-slim@sha256:0bc9ce8b3c40e7892a575cd44ea16c673ac497c6eb0e6a51aa40ee3d85033bcb                  0.0s
 => [internal] load build context                                                                                                         0.0s
 => => transferring context: 191.02kB                                                                                                     0.0s
 => CACHED [2/7] WORKDIR /app                                                                                                             0.0s
 => CACHED [3/7] RUN apt-get update     && apt-get upgrade -y     && apt-get install -y gcc default-libmysqlclient-dev pkg-config     &&  0.0s
 => CACHED [4/7] COPY requirements.txt .                                                                                                  0.0s
 => CACHED [5/7] RUN pip3 install mysqlclient                                                                                             0.0s
 => CACHED [6/7] RUN pip3 install --no-cache-dir -r requirements.txt                                                                      0.0s
 => CACHED [7/7] COPY . .                                                                                                                 0.0s
 => exporting to image                                                                                                                    0.0s
 => => exporting layers                                                                                                                   0.0s
 => => writing image sha256:206217c69d38de296781e54495ed99972314362c39ce8f52111e6831a9c25a7c                                              0.0s
 => => naming to docker.io/library/two-tier-flask-app-flask                                                                               0.0s
 => resolving provenance for metadata file                                                                                                0.0s
[+] Running 4/4
 ✔ two-tier-flask-app-flask             Built                                                                                             0.0s 
 ✔ Network two-tier-flask-app_two-tier  Created                                                                                           0.0s 
 ✔ Container mysql                      Started                                                                                           0.4s 
 ✔ Container two-tier-backend           Started                                                                                           0.2s

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker ps
CONTAINER ID   IMAGE                      COMMAND                  CREATED         STATUS                            PORTS                                         NAMES
73001a53d865   two-tier-flask-app-flask   "python app.py"          9 seconds ago   Up 8 seconds (health: starting)   0.0.0.0:5001->5000/tcp, [::]:5001->5000/tcp   two-tier-backend
ee5122edf81b   mysql                      "docker-entrypoint.s…"   9 seconds ago   Up 8 seconds (healthy)            0.0.0.0:3306->3306/tcp, [::]:3306->3306/tcp   mysql


raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker compose down
WARN[0000] /Users/raghavendracn/Documents/Docker/two-tier-flask-app/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 3/3
 ✔ Container two-tier-backend           Removed                                                                                           0.2s 
 ✔ Container mysql                      Removed                                                                                           0.8s 
 ✔ Network two-tier-flask-app_two-tier  Removed

```
