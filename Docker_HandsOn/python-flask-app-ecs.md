## PYTHON PROJECT FLASK APP ECS USING DOCKER

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % git clone https://github.com/LondheShubham153/flask-app-ecs.git
Cloning into 'flask-app-ecs'...
remote: Enumerating objects: 18, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 18 (delta 3), reused 2 (delta 2), pack-reused 9 (from 1)
Receiving objects: 100% (18/18), done.
Resolving deltas: 100% (3/3), done.


raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % ls
docker_practise_logs.txt flask-app-ecs            hello-docker             java-project             mysql
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % cd flask-app-ecs 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % ls
app.py           Dockerfile       Dockerfile-multi README.md        requirements.txt run.py
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % mv Dockerfile Dockerfile_backup
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % vim Dockerfile

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % cat Dockerfile
FROM python:3.7

WORKDIR /app

COPY . .

RUN pip3 install -r requirements.txt

ENTRYPOINT ["python","run.py"]
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker build -t flask-app .
[+] Building 1.6s (10/10) FINISHED                                                                                        docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 147B                                                                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.7                                                                             1.6s
 => [auth] library/python:pull token for registry-1.docker.io                                                                             0.0s
 => [internal] load .dockerignore                                                                                                         0.0s
 => => transferring context: 2B                                                                                                           0.0s
 => [1/4] FROM docker.io/library/python:3.7@sha256:eedf63967cdb57d8214db38ce21f105003ed4e4d0358f02bedc057341bcf92a0                       0.0s
 => [internal] load build context                                                                                                         0.0s
 => => transferring context: 2.17kB                                                                                                       0.0s
 => CACHED [2/4] WORKDIR /app                                                                                                             0.0s
 => CACHED [3/4] COPY . .                                                                                                                 0.0s
 => CACHED [4/4] RUN pip3 install -r requirements.txt                                                                                     0.0s
 => exporting to image                                                                                                                    0.0s
 => => exporting layers                                                                                                                   0.0s
 => => writing image sha256:d55838f3af5113e3c491f149fa7fab1dfae2c7ff7350cce7247b926106aaadaa                                              0.0s
 => => naming to docker.io/library/flask-app                                                                                              0.0s

View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/i7e3qkxq526eb91rej54e3ngp

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % 


```

```

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker run -p 80:80 flask-app
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:80
 * Running on http://172.17.0.2:80
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 488-920-868
192.168.65.1 - - [09/Oct/2025 01:43:45] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:43:45] "GET /favicon.ico HTTP/1.1" 404 -

```

## open the url http://127.0.0.1:80 in browser and will display like

Hello Dosto, welcome to DevOps Zero To Hero (Junoon Batch 9)

# DOCKER LOGS COMMAND TO Check the logsof docker image

command
```
docker logs f223f9635136
```
```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker run -d -p 80:80 flask-app
f223f96351364881c3a69317ac0ff0e38165e8c367a4277aaf12d087c080047e
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker ps
CONTAINER ID   IMAGE       COMMAND           CREATED         STATUS         PORTS                                 NAMES
f223f9635136   flask-app   "python run.py"   5 seconds ago   Up 5 seconds   0.0.0.0:80->80/tcp, [::]:80->80/tcp   practical_chaum
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker logs f223f9635136                                            
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:80
 * Running on http://172.17.0.2:80
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 965-224-708
```

# DOCKER ATTACH COMMAND is used to check the how many times browser got refresh

command

```
docker attach f223f9635136
```


```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker attach f223f9635136 
192.168.65.1 - - [09/Oct/2025 01:52:03] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:52:09] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:52:09] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:52:09] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:52:10] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:52:10] "GET / HTTP/1.1" 200 -
192.168.65.1 - - [09/Oct/2025 01:52:10] "GET / HTTP/1.1" 200 -

```

# Docker start and stop command used to run the image using the same created image id

COMMAND
```
docker stop <docker image id>

docker start <docker image id>
```


```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker stop f223f9635136
f223f9635136
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker start f223f9635136
f223f9635136
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker ps
CONTAINER ID   IMAGE       COMMAND           CREATED         STATUS         PORTS                                 NAMES
f223f9635136   flask-app   "python run.py"   7 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   practical_chaum

```
