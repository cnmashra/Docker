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
