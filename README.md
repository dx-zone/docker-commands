### Docker Commands Summary from the Book, Docker: Practical Guide for Developers and DevOps Teams, by Bernd Oggl, Rheinwerk Computing.

### Docker: Practical Guide for Developers and DevOps Teams

```bash
# Show the Docker version information
docker version

# List all containers and show their sizes
docker ps -a -s

# Run a temporary alpine container interactively, removing it after exit
docker run -it --rm alpine

# Run a Docker container from the specified image
docker run <docker-image-name>

# Run a Docker container using the hello-world image
docker run hello-world

# List all containers, including stopped ones
docker ps -a

# Remove the Docker image named 'helo-world'
docker image rm helo-world

# Run a hello-world container and remove it after it exits
docker run --rm hello-world

# Run a Docker container interactively from the specified image
docker run -it <image-name>

# Pull the specified image from a Docker registry
docker image pull <image-name>

# Start a Docker container interactively from the specified image
docker start -i <image-name>

# Stop the specified Docker container
docker stop <container-name>

# Run a Docker container interactively with a custom name and hostname
docker run -it --name <custom-name> -h <custom-hostname> <image-name>

# Start an interactive session with a Docker container with a custom name
docker start -i <custom-name>

# Execute the 'top' command interactively inside the specified container
docker exec -it <container-name> /usr/bin/top

# Display detailed information about the specified container
docker inspect <container-name>

# Display mounted volumes of the specified container using a format option
docker inspect -f  '{{ .Mounts }}' <container-name>

# Inspect a specific Docker volume by name or ID
docker volume inspect <volume-name-or-volume-id>

# Start an interactive Bash shell inside the specified Docker container
docker exec -it <container-name> /bin/bash

# Display logs for the specified Docker container
docker logs <container-name>

# Remove the specified Docker volume by name or ID
docker volume rm <volume-name-or-volume-id>

# Delete unused and dissociated volumes
docker volume prune

# List all Docker images available locally
docker images

# Remove the specified Docker image
docker image rm <image-name>

# Force remove the specified Docker image
docker image rm -f <image-name>

# Remove the Docker image
docker rmi <image-name>

# Force remove the specified Docker image
docker rmi -f <image-name>

# List IDs of all dangling volumes (unused and not associated with any containers)
docker volume ls -q -f dangling=true

# Show Docker disk usage statistics
docker system df


## Workflow for new deployments: Download an image, make changes, save the changes, backup, and publish the image ##

# Pull the latest Ubuntu image from Docker Hub
docker pull ubuntu:latest

# Run a container interactively from the latest Ubuntu image and access its shell
docker run -it ubuntu:latest /bin/bash

# Update the package list inside the container
apt-get update

# Install nginx inside the container
apt-get install nginx

# Commit the changes made in the container to create a new image with nginx installed
docker commit -m "Installed nginx" -a "Your Name" <container-id> yourname/ubuntu-nginx:latest

# Save the new Docker image to a tar file for backup or transfer
docker save -o ubuntu-nginx-latest.tar yourname/ubuntu-nginx:latest

# Log in to a Docker registry (replace [registry-url] with actual URL)
docker login [registry-url]

# Tag the new image with the registry URL, username, and tag (fix syntax by completing the command)
docker tag yourname/ubuntu-nginx:latest <registry-url>/<username>/ubuntu-nginx:latest

# Push the tagged image to the specified Docker registry
docker push <registry-url>/<username>/ubuntu-nginx:latest

# Save an image to a tar file, specifying the image name and output file
docker save -o <path_to_output_tar_file>.tar <image_name>:


```



# Commit changes made to a container into a new image with additional options like message and author



1. **Download an Image**:
   - `docker pull ubuntu:latest` downloads the latest Ubuntu base image from Docker Hub.
2. **Make Changes**:
   - Running `docker run -it ubuntu:latest /bin/bash` allows you to start a container and make changes interactively.
   - `apt-get update` and `apt-get install nginx` are examples of making changes by updating the package lists and installing new software (nginx in this case).
3. **Save the Changes**:
   - `docker commit -m "Installed nginx" -a "Your Name" <container-id> yourname/ubuntu-nginx:latest` saves the state of the container as a new image, preserving the modifications made.
4. **Backup**:
   - `docker save -o ubuntu-nginx-latest.tar yourname/ubuntu-nginx:latest` creates a tarball of the new image, effectively backing it up for storage or transfer.
5. **Publish the Image**:
   - `docker login [registry-url]` logs you into a Docker registry.
   - `docker tag yourname/ubuntu-nginx:latest <registry-url>/<username>/ubuntu-nginx:latest` tags the new image with the registry URL, preparing it for publication.
   - `docker push <registry-url>/<username>/ubuntu-nginx:latest` publishes the tagged image to the specified Docker registry, making it available for further distribution or deployment.

```bash
# Workflow Summary with Ubuntu Linux as Example
docker pull ubuntu:latest
docker run -it ubuntu:latest /bin/bash
apt-get update
apt-get install nginx
docker commit -m "Installed nginx" -a "Your Name" <container-id> yourname/ubuntu-nginx:latest
docker save -o ubuntu-nginx-latest.tar yourname/ubuntu-nginx:latest

docker login [registry-url]
docker tag <image_name>:
docker push <registry-url>/<username>/<image_name>:

# Create a new image from a container's current state. Essentially, it captures the modifications you've made to a running container and saves them as a new image.
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
docker save -o <path_to_output_tar_file>.tar <image_name>:

```%  
