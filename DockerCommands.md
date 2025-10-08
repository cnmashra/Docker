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
