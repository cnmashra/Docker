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
