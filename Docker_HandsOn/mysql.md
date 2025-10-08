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

#STEPS AND SYNTAX

## 🧩 Step 1: Check if MySQL is running
Run:
```
docker ps
```

## 🧩 Step 2: Log in to MySQL inside the container
Use this command:

```
docker exec -it <container_id> mysql -u root -p
```
Then enter your MySQL root password (the one you set during container creation, e.g., via -e MYSQL_ROOT_PASSWORD=my-secret-pw).

Example:
```
docker exec -it mysql mysql -u root -p
```

## 🧩 Step 3: If you forgot the root password

You can reset it by restarting MySQL with a temporary override:
```
docker exec -it <container_id> bash
```

Then inside the container:

```
mysql -u root
```

If still denied, stop the container and restart MySQL in safe mode:
```
'docker stop mysql
docker run --name mysql --rm -e MYSQL_ROOT_PASSWORD=root -d mysql
```
Now try again:

```
docker exec -it mysql mysql -u root -proot
```

## 🧩 Step 4: (Optional) Create a new user

Once logged in:

```
CREATE USER 'admin'@'%' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

```
Now you can connect with:

```
mysql -u admin -ppassword123

```

### Perfect ✅ — here’s a ready-to-use Docker command to spin up a fresh MySQL container with a known password, persistent storage, and proper configuration 👇

## 🐳 Run a new MySQL container (clean setup)

```
docker run -d \
  --name mysql-server \
  -e MYSQL_ROOT_PASSWORD=Root@123 \
  -e MYSQL_DATABASE=demo_db \
  -e MYSQL_USER=demo_user \
  -e MYSQL_PASSWORD=Demo@123 \
  -p 3306:3306 \
  -v $HOME/mysql_data:/var/lib/mysql \
  mysql:latest

```

🧩 Explanation:

```

| Option                               | Purpose                                           |
| ------------------------------------ | ------------------------------------------------- |
| `--name mysql-server`                | Container name for easy reference                 |
| `-e MYSQL_ROOT_PASSWORD=Root@123`    | Sets root password                                |
| `-e MYSQL_DATABASE=demo_db`          | Automatically creates a database named `demo_db`  |
| `-e MYSQL_USER=demo_user`            | Creates a user named `demo_user`                  |
| `-e MYSQL_PASSWORD=Demo@123`         | Sets that user’s password                         |
| `-p 3306:3306`                       | Exposes MySQL port to host                        |
| `-v $HOME/mysql_data:/var/lib/mysql` | Persists MySQL data on your Mac in `~/mysql_data` |

```
## 🧠 Verify that it’s running

```
docker ps

```
You should see:

```
CONTAINER ID   IMAGE       COMMAND                  PORTS                    NAMES
123abc...      mysql:latest   "docker-entrypoint..."   0.0.0.0:3306->3306/tcp   mysql-server

```
## 🧑‍💻 Log in to MySQL
```
docker exec -it mysql-server mysql -u root -p

```
Enter password:
```
Root@123
```

✅ You should now see the MySQL prompt:

```
mysql>

```
