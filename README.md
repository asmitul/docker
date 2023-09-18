# docker


1. [Install Docker Engine on Ubuntu 22.04](#install-docker-engine-on-ubuntu-22-04)
2. [Install Docker on Debian 11](#install-docker-engine-on-debian-11)
3. [How to Use APP With Docker](#how-to-use-app-with-docker)

### Install Docker Engine on Ubuntu 22.04

Run the following command to uninstall all conflicting packages:
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
Add Docker's official GPG key:
```bash
sudo apt-get update
```
```bash
sudo apt-get install ca-certificates curl gnupg
```
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```


Add the repository to Apt sources:
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```bash
sudo apt-get update
```
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Install Docker Engine on Debian 11
Run the following command to uninstall all conflicting packages:
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
Add Docker's official GPG key:
```bash
sudo apt-get update
```
```bash
sudo apt-get install ca-certificates curl gnupg
```
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
Add the repository to Apt sources:
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```bash
sudo apt-get update
```
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### How to Use APP With Docker
goto docker hub to find the official docker image
and pull it
```bash
docker pull image_name
```

create app network
```bash
docker network create app_name_network
```
```bash
# docker run \
#   --name jenkins-docker \         # create container name
#   --restart=unless-stopped \      # restart container
#   --detach \                      # run container in background
#   --privileged \                  # run container in privileged mode
#   --network jenkins \             # attach container to network
#   --network-alias docker \        # set container alias
#   --env DOCKER_TLS_CERTDIR=/certs \                   # set environment
#   --volume jenkins-docker-certs:/certs/client \       # set volume
#   --volume jenkins-data:/var/jenkins_home \           # set volume
#   --publish 2376:2376 \           # publish port
#   --publish 8080:8080 \           # publish port
#   --publish 50000:50000 \         # publish port
#   jenkins/jenkins:jdk17           # image name 
```
```bash
docker run \
  --name container_name \
  --restart=unless-stopped \
  --detach \
  --privileged \
  --network app_name_network \
  --env ENVIRONMENT=dev \
  --volume localpath:dockerpath \
  --publish outsideport:dockerinsideport \
  image_name
```
