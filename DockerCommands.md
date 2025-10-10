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
