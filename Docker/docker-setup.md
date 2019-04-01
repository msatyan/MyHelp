### [Docker](https://www.docker.com/)
- [Dcoc](https://docs.docker.com/)


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

### Delete all Containers
```bash
sudo docker system prune
```
