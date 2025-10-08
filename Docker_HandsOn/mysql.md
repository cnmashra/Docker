### STEPS TO INSTALL AND ACCESS THE MYSQL DOCKER

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/mysql % docker run -d -e MYSQL_ROOT_PASSWORD=root mysql
b33f7106944b25d7ae7d4b711ccc18ca91619feee89e0ae720cae1b0f328b564
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/mysql % docker exec -it b33f7106944b mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 9.4.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
