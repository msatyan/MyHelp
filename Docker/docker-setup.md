### [Docker](https://www.docker.com/)
- [Dcoc](https://docs.docker.com/)
- [Commands](https://docs.docker.com/engine/reference/commandline/docker/)
- [Docker for beginners](https://docker-curriculum.com/)
- [Basic Commands](https://rominirani.com/docker-tutorial-series-part-2-basic-commands-baaf70807fd3)

### [Docker Setup on Ubuntu 18.04 LTS](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce)




- Check the OS version
```
cat /etc/*release*
```


### Un Install

```bash
# Uninstall old versions if any
sudo apt-get remove docker docker-engine docker.io
```


### Install Docker CE
```bash
# Update the apt package index 
sudo apt-get update

# Install packages to allow apt to use a repository over HTTPS:
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

# Add Docker’s official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -


# Verify that you now have the key with the fingerprint
sudo apt-key fingerprint 0EBFCD88

# Use the following command to set up the stable repository.
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# INSTALL DOCKER CE
# Install Docker from the Docker Repository
sudo apt-get update
# sudo apt-get install docker-ce
sudo apt-get install docker-ce docker-ce-cli containerd.io

# If you want to install docker version from the Ubuntu repository
# sudo apt install docker.io

# Wait until the installation has been completed, then you can start Docker and add it to the boot time with the systemctl command:

systemctl start docker
systemctl enable docker

docker --version
```

### Run a Hello World
```bash
# run = create + start
sudo docker run hello-world
# or
sudo docker run busybox echo my hello world
```

### The -it flag
```bash
# Running the run command with the -it flags attaches us to an interactive tty in the container.
# -i, --interactive
# -t, --tty
sudo docker run -it busybox sh
```


### useful commands
```bash
sudo docker ps
sudo docker ps -a

# help ?
sudo docker     --help
sudo docker run --help

# basic list
docker run – Runs a command in a new container.
docker start – Starts one or more stopped containers
docker stop – Stops one or more running containers
docker build – Builds an image form a Docker file
docker pull – Pulls an image or a repository from a registry
docker push – Pushes an image or a repository to a registry
docker export – Exports a container’s filesystem as a tar archive
docker exec – Runs a command in a run-time container
docker search – Searches the Docker Hub for images
docker attach – Attaches to a running container
docker commit – Creates a new image from a container’s changes
```

### Delete Containers
```bash
# get the id
sudo docker ps -a

# Deleting a specific set with id
sudo docker rm  0b525655e3eb 1943a6a72b3b

# also checkout the following
sudo docker container prune
sudo docker system prune
```
