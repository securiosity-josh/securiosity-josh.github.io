---
title: "Ubuntu: Setup & Install Docker"
date: 2025-10-27 08:00:00 +0000
categories: [homelab, administration]
tags: [docker]     # TAG names should always be lowercase
image:
  path: /assets/img/headers/docker.webp
---


This is more for my reference than anything else, but here are the steps to install Docker on Ubuntu.

## Cleaning up old versions

if we have any old/existing versions of Docker installed, we should remove them first:

```shell
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

## Installing Docker
Now we can install Docker by following these steps:
```shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
> *If you use an Ubuntu derivative distro, such as Linux Mint, you may need to use `UBUNTU_CODENAME` instead of `VERSION_CODENAME`.*
{: .prompt-info }

### Install the latest version of Docker Engine and containerd
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Check installed version
```shell
docker -v
``` 

### Check Docker Compose
```shell
docker compose
``` 

### Use Docker without sudo
To avoid using `sudo` with every Docker command, add your user to the `docker` group:
```shell
sudo usermod -aG docker $USER
```

You’ll need to log out then back in to apply this change.