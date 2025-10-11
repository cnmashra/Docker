# IMPOTANT DOCKER COMMANDS LIST FOR REFERNENCE

### Option 1: Remove a specific image by name or ID

```
docker rmi <image_id>

OR

docker rmi <repository>:<tag>

Example

docker rmi mysql:latest
docker rmi abhishekf5/cicd-e2e:33
docker rmi 90ec22e21be2   # Using IMAGE ID

```

### 🧨 Option 2: Force remove (if image is used by a stopped container)

If you get an error like:

"image is being used by stopped container"

Run:

```
docker rmi -f <image_id>
```

### 🧽 Option 3: Remove all Docker images

```
docker rmi -f $(docker images -q)

```
### 🪣 Option 4: Clean up everything unused

```
docker system prune -a
```
Then confirm by typing y.

### 🧾 Optional: Verify cleanup

After cleanup, check remaining images:

```
docker images

```

# SCRIPT TO CLEAN UP THE DOCKER IMAGES

## docker-cleanup.sh

```
#!/bin/bash

# ========================================
# 🧹 Docker Cleanup Script - Safe Version
# ========================================

echo "🚀 Starting Docker cleanup..."

# Step 1: Stop all running containers
echo "🛑 Stopping running containers..."
docker stop $(docker ps -q) 2>/dev/null || echo "No running containers found."

# Step 2: Remove all stopped containers
echo "🗑 Removing stopped containers..."
docker container prune -f

# Step 3: Remove dangling (unused) images
echo "🧽 Removing dangling images..."
docker image prune -f

# Step 4: Remove unused networks
echo "🌐 Removing unused networks..."
docker network prune -f

# Step 5: (Optional) Remove all unused images
read -p "❗ Do you want to remove ALL unused images? (y/n): " remove_all
if [ "$remove_all" = "y" ]; then
    echo "🧨 Removing ALL unused images..."
    docker image prune -a -f
else
    echo "✅ Skipping full image cleanup."
fi

# Step 6: (Optional) Remove unused volumes
read -p "❗ Do you want to remove unused volumes? (y/n): " remove_volumes
if [ "$remove_volumes" = "y" ]; then
    echo "📦 Removing unused volumes..."
    docker volume prune -f
else
    echo "✅ Skipping volume cleanup."
fi

# Step 7: Final cleanup summary
echo "✨ Final cleanup summary:"
docker system df

echo "✅ Docker cleanup completed successfully!"

```

# To run the docker container in background continuously untill stop use below command

COMMAND

```
docker run -itd <docker image name>

```

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker run -itd ubuntu
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
7bdf644cff2e: Already exists 
Digest: sha256:728785b59223d755e3e5c5af178fab1be7031f3522c5ccd7a0b32b80d8248123
Status: Downloaded newer image for ubuntu:latest
a762bf43e276d4708e842dcc7195405e28bd00cb496d0d14dce4e50b75381e7d
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
a762bf43e276   ubuntu    "/bin/bash"   6 seconds ago   Up 6 seconds             quirky_maxwell
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker stop a762bf43e276
a762bf43e276
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs %

```

## docker command to remove all unused container and volume in the system

command
```
docker system prune

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - unused build cache

Are you sure you want to continue? [y/N] y
Deleted Containers:
701f2e909c5d7a8f06b4362b365c273635eb69298587060663b280d8bcf86dbd
e00572b2b5cfc1f6a98af80a002cbda4fb45dc6bc49a92dfcafcb200a6db8800
a762bf43e276d4708e842dcc7195405e28bd00cb496d0d14dce4e50b75381e7d
f223f96351364881c3a69317ac0ff0e38165e8c367a4277aaf12d087c080047e
fbb95c41cb206a2cfa01bf5f714f9a063168375f9b2bfde3396195a0d4bae2b7
82f070376085c47fe3222d8f6072449d5d68990ed8fae06858bed6ae40d0ed9f
5e58231080088b42c9563277ecbda608a7646d0a7851b8f13b26877173dec67d
7c2f4e4c5ff24e9a71d6594ce79d1ba236c963532716eb3b11de693b84b39b8c
81c0cd7146899fc9d3ce9af4fb60c0ee3f9630ebe1877f6f9f9452b1e651b90b
8c02b328f8fd51214b4fdee464cda8545584ab6caf9a652d6138bf14eaec93c7
b33f7106944b25d7ae7d4b711ccc18ca91619feee89e0ae720cae1b0f328b564
1e56167229a93bee7004b37cf1c93abec36ed3337f8f38afda7ca2c1ba14868a

Deleted Networks:
two-tier
mynetwork

Deleted Images:
deleted: sha256:d55838f3af5113e3c491f149fa7fab1dfae2c7ff7350cce7247b926106aaadaa

Deleted build cache objects:
5l22dhrou3buweldmusdty8nt
jfeuakcizpxa652b8xvurpmwg
kf8wo97uv9kedzhpbg5wq22vd
kktfl7bkif5bvedxfcl6aptrx
q9rugmrg338dw29ak4d5d2uhm
bxshlix52l3mbl23vnlsb3pki
p04hw2ij9nsmsw5iiyezrq29p
0ms6xmhb0wdih3gvl0ddj4wnv
25n9cr4v9u0xc0zqxna4nan9o
lq40dfrbzxncd0axua4uvo8fq
op6vl9uogx5re83jxs12vxmq5
1h9j4tmjjhzhj0ril4lmacplh
668wvq3k837kzh5o0zco9eb66
475yvkmfgmwvvzxzwp447nrea
7cddomfkcxzx4wuuc4h5th7j7

Total reclaimed space: 12.5MB
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 

```

### command to list all the docker image id
command
```
docker images -ag
```

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker images -aq
206217c69d38
84a3832189d4
ba9f9a6fcaf3
abbf8b88d6a0
c3cee4aaf374
90ec22e21be2
d598f2517351
```

### command to remove all the docker images at a time

command

```
docker rmi -f $(docker images -aq)
```


raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker rmi -f $(docker images -aq)
Untagged: two-tier-flask-app-flask:latest
Deleted: sha256:206217c69d38de296781e54495ed99972314362c39ce8f52111e6831a9c25a7c
Untagged: two-tier-backend:latest
Deleted: sha256:84a3832189d495dfd983f251e7f91c05a7e737f180a57d8c5035598c622cddd1
Untagged: flask-app:latest
Deleted: sha256:ba9f9a6fcaf364144507e136474efd9bcbc782f672faaa80fbb59ec695a9cfae
Untagged: java-app:latest
Deleted: sha256:abbf8b88d6a0e9c956aa6e6e33c68ada43615e4a3493eec4f35585f2a5988302
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:728785b59223d755e3e5c5af178fab1be7031f3522c5ccd7a0b32b80d8248123
Deleted: sha256:c3cee4aaf374d53303679d87528ae4ad32df1e8d990e482599dc5646d240349e
Untagged: mysql:latest
Untagged: mysql@sha256:91447968e66961302339ec4dc4d385f5e1a957d98e63c7d52ecf8b1de0907346
Deleted: sha256:90ec22e21be27435c6991930424ae28428cd09c82d7928e2c4e5810de8849ccb
Deleted: sha256:d04847decb00633b8f05ba495194dee37ef5c3981141bac71f950991303e14aa
Deleted: sha256:5ac68f0c087420896e4fcb4a1444289d398b34ce5a1087454ca5ecc175f5d26c
Deleted: sha256:3d761445152993caf4e81232f2daa6f2cd7efd9a22943e92e1586521081ff6c5
Deleted: sha256:025e1fc3a7ef67b90d9b301596dbc002122c866db5480f99c53bbe1ee7776aa5
Deleted: sha256:1b4cd381863c7236ba92026b99753a3f3e1d99192c9b88ff799a1c9ff566d260
Deleted: sha256:f660ffbdad6212b82401dec844b3bced91002658fdc36e11742d6efa729b1ea6
Deleted: sha256:80f274026908724bb12799af59f4adc3fb4ef597db462fc9f3c47d77256b3134
Deleted: sha256:de0c126eea868ec1026e97a2c1348a66792f3f4b06871f0e5d176bd1a998c44c
Deleted: sha256:cbf52a700d7a887b0b05264972664fc3baf260cb699c6cae78b61632ac4317c0
Deleted: sha256:926ca09e80338405c67b56c2a53c40c6cbfd65d36c44dfa4bcbca01418346a84
Untagged: justincormack/nsenter1:latest
Untagged: justincormack/nsenter1@sha256:e876f694a4cb6ff9e6861197ea3680fe2e3c5ab773a1e37ca1f13171f7f5798e
Deleted: sha256:d598f2517351c243ce73e368bd7d4499cf8e4a74cd94b0e261edaf722583e403
Deleted: sha256:b040f551814915e6b8dd08cbe0cc7ff5475bb92ef0389a735de4220168f1e31d
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 

```
