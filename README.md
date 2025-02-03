
#!/bin/bash

# Stop all running containers
echo "Stopping all running containers..."

docker stop $(docker ps -aq) 2>/dev/null

# Remove all containers
echo "Removing all containers..."

docker rm $(docker ps -aq) 2>/dev/null

# Clean up unused containers
echo "Pruning unused containers..."

docker container prune -f 2>/dev/null

# Remove all images
echo "Removing all Docker images..."

docker rmi $(docker images -q) 2>/dev/null

# Clean up unused images
echo "Pruning unused images..."

docker image prune -af 2>/dev/null

# Remove all volumes
echo "Removing all volumes..."

docker volume rm $(docker volume ls -q) 2>/dev/null

# Clean up unused volumes
echo "Pruning unused volumes..."

docker volume prune -f 2>/dev/null

# Remove all networks (excluding the default ones like bridge, host, and none)
echo "Removing all Docker networks..."

docker network rm $(docker network ls -q | grep -vE '^(bridge|host|none)$') 2>/dev/null

# Clean up unused networks
echo "Pruning unused networks..."

docker network prune -f 2>/dev/null

# Remove all Docker config maps (for Docker Swarm, if used)
echo "Removing all Docker config maps..."

docker config rm $(docker config ls -q) 2>/dev/null

# Remove all Docker secrets (for Docker Swarm, if used)
echo "Removing all Docker secrets..."

docker secret rm $(docker secret ls -q) 2>/dev/null

# Clean up unused Docker secrets (for Docker Swarm)
echo "Pruning unused Docker secrets..."

docker secret prune -f 2>/dev/null

echo "Cleanup completed successfully."
