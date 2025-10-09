# Docker Network project Two tier application (Appliation between flask and mysql)

```

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % git clone https://github.com/LondheShubham153/two-tier-flask-app.git
Cloning into 'two-tier-flask-app'...
remote: Enumerating objects: 451, done.
remote: Total 451 (delta 0), reused 0 (delta 0), pack-reused 451 (from 1)
Receiving objects: 100% (451/451), 116.06 KiB | 1.33 MiB/s, done.
Resolving deltas: 100% (226/226), done.
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % ls
docker_practise_logs.txt hello-docker             mysql
flask-app-ecs            java-project             two-tier-flask-app

```

app.py complete code

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % ls
app.py                Dockerfile-multistage Jenkinsfile           message.sql           templates
docker-compose.yml    dummy.txt             k8s                   README.md
Dockerfile            eks-manifests         Makefile              requirements.txt
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % cat app.py 
import os
from flask import Flask, render_template, request, redirect, url_for, jsonify
from flask_mysqldb import MySQL

app = Flask(__name__)

# Configure MySQL from environment variables
app.config['MYSQL_HOST'] = os.environ.get('MYSQL_HOST', 'localhost')
app.config['MYSQL_USER'] = os.environ.get('MYSQL_USER', 'default_user')
app.config['MYSQL_PASSWORD'] = os.environ.get('MYSQL_PASSWORD', 'default_password')
app.config['MYSQL_DB'] = os.environ.get('MYSQL_DB', 'default_db')

# Initialize MySQL
mysql = MySQL(app)

def init_db():
    with app.app_context():
        cur = mysql.connection.cursor()
        cur.execute('''
        CREATE TABLE IF NOT EXISTS messages (
            id INT AUTO_INCREMENT PRIMARY KEY,
            message TEXT
        );
        ''')
        mysql.connection.commit()  
        cur.close()

@app.route('/')
def hello():
    cur = mysql.connection.cursor()
    cur.execute('SELECT message FROM messages')
    messages = cur.fetchall()
    cur.close()
    return render_template('index.html', messages=messages)

@app.route('/submit', methods=['POST'])
def submit():
    new_message = request.form.get('new_message')
    cur = mysql.connection.cursor()
    cur.execute('INSERT INTO messages (message) VALUES (%s)', [new_message])
    mysql.connection.commit()
    cur.close()
    return jsonify({'message': new_message})

if __name__ == '__main__':
    init_db()
    app.run(host='0.0.0.0', port=5000, debug=True)

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app %

```


Dockerfile details

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % cat Dockerfile
# Use an official Python runtime as the base image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# install required packages for system
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y gcc default-libmysqlclient-dev pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Copy the requirements file into the container
COPY requirements.txt .

# Install app dependencies
RUN pip3 install mysqlclient
RUN pip3 install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Specify the command to run your application
CMD ["python", "app.py"]

```

# Creating a Docker image of the Two-Tier-backend project

```

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker build -t two-tier-backend .
[+] Building 57.2s (13/13) FINISHED                                                                                       docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 669B                                                                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.9-slim                                                                        3.1s
 => [auth] library/python:pull token for registry-1.docker.io                                                                             0.0s
 => [internal] load .dockerignore                                                                                                         0.0s
 => => transferring context: 2B                                                                                                           0.0s
 => [1/7] FROM docker.io/library/python:3.9-slim@sha256:151b796af055298f244bc4d203bc19e19b0e63c8aa26c4fed2fc6809ea9b7caf                  9.0s
 => => resolve docker.io/library/python:3.9-slim@sha256:151b796af055298f244bc4d203bc19e19b0e63c8aa26c4fed2fc6809ea9b7caf                  0.0s
 => => sha256:151b796af055298f244bc4d203bc19e19b0e63c8aa26c4fed2fc6809ea9b7caf 10.36kB / 10.36kB                                          0.0s
 => => sha256:de8c489864741b913f20a0fc6378a1d386df88076cf511f00ae35979259946cb 1.75kB / 1.75kB                                            0.0s
 => => sha256:b1a7a0b67e7215a323e98da295687cd886d385df23a22276f569788a00d6b571 5.32kB / 5.32kB                                            0.0s
 => => sha256:e363695fcb930d5f18449254c0052117582c3de4263c91575b0a9040c986e412 30.14MB / 30.14MB                                          7.7s
 => => sha256:815fda8de65a3ddc949c8c3fb9ee6871e2057a7f46bc44c33bcb598aaf8d476a 1.27MB / 1.27MB                                            1.9s
 => => sha256:8b523f2468e2187932babe4a629863e7b9509bddaa9c40b1e3fc83bc6cb9863d 13.31MB / 13.31MB                                          4.2s
 => => sha256:4bff20198c4500a7da762ddfff1ff0632ef6556680cb6bd1cf1daeb5f2995d99 249B / 249B                                                2.3s
 => => extracting sha256:e363695fcb930d5f18449254c0052117582c3de4263c91575b0a9040c986e412                                                 0.7s
 => => extracting sha256:815fda8de65a3ddc949c8c3fb9ee6871e2057a7f46bc44c33bcb598aaf8d476a                                                 0.1s
 => => extracting sha256:8b523f2468e2187932babe4a629863e7b9509bddaa9c40b1e3fc83bc6cb9863d                                                 0.4s
 => => extracting sha256:4bff20198c4500a7da762ddfff1ff0632ef6556680cb6bd1cf1daeb5f2995d99                                                 0.0s
 => [internal] load build context                                                                                                         0.0s
 => => transferring context: 189.97kB                                                                                                     0.0s
 => [2/7] WORKDIR /app                                                                                                                    0.1s
 => [3/7] RUN apt-get update     && apt-get upgrade -y     && apt-get install -y gcc default-libmysqlclient-dev pkg-config     && rm -r  37.1s
 => [4/7] COPY requirements.txt .                                                                                                         0.0s 
 => [5/7] RUN pip3 install mysqlclient                                                                                                    3.9s 
 => [6/7] RUN pip3 install --no-cache-dir -r requirements.txt                                                                             3.5s 
 => [7/7] COPY . .                                                                                                                        0.0s 
 => exporting to image                                                                                                                    0.4s 
 => => exporting layers                                                                                                                   0.4s 
 => => writing image sha256:84a3832189d495dfd983f251e7f91c05a7e737f180a57d8c5035598c622cddd1                                              0.0s 
 => => naming to docker.io/library/two-tier-backend                                                                                       0.0s 
                                                                                                                                               
View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/tq02pr3e85jye8sqpuht35hhx

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 

```

# Steps to install MYSQL project

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
ecb83b09a418: Already exists 
91beec75ea95: Already exists 
113f24e83af6: Already exists 
20e973ad942c: Already exists 
49bbd3f4ed8c: Already exists 
ecd21296720f: Already exists 
fbda0e12a0b6: Already exists 
42a31c1f092c: Already exists 
716452459d78: Already exists 
ae25a9a46a8f: Already exists 
Digest: sha256:91447968e66961302339ec4dc4d385f5e1a957d98e63c7d52ecf8b1de0907346
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview mysql
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker run -d -e MYSQL_ROOT_PASSWORD=root mysql
e52135e6e4d52ccc21cc5b072a38dbd8268e24dc665197e6519f8d037013c8d6
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                 NAMES
e52135e6e4d5   mysql     "docker-entrypoint.s…"   7 seconds ago   Up 6 seconds   3306/tcp, 33060/tcp   boring_taussig
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % 

```

## Steps to create the devops database inside the mysql instance

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker exec -it e52135e6e4d5 bash
bash-5.1# mysql -u root -proot
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 9.4.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.010 sec)

mysql> create database devops;
Query OK, 1 row affected (0.008 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| devops             |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.002 sec)

mysql> 
mysql> exit
Bye
bash-5.1# exit
exit

What's next:
    Try Docker Debug for seamless, persistent debugging tools in any container or image → docker debug e52135e6e4d5
    Learn more at https://docs.docker.com/go/debug-cli/

```
