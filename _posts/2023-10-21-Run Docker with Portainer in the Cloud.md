---
title: Run Docker with Portainer in the Cloud
image: ![Docker](/assets/docker.png)
date: 2023-10-21
categories: [cloud]
tags: [cloud]
---
![Docker](/assets/docker.png)

*Docker is a containerization platform that allows you to package 
applications and their dependencies into lightweight, isolated containers. 
These containers can run consistently across different environments, 
making it easier to deploy and manage applications.*


![Portainer](/assets/portainer.png)

*Portainer is an open-source container management platform that simplifies the 
deployment, monitoring, and management of Docker containers.
It provides a graphical interface to streamline container orchestration tasks, 
making it accessible for both beginners and experienced developers.*

For this installation, I will be using Ubuntu as my distribution of choice.
The below commands will work on any Debian-based distribution.


Step 1

Access your cloud instance via SSH and update the repositories.


```
sudo apt update -y
```

```
sudo apt upgrade -y
```

Step 2

Install Docker & Docker compose 


```
sudo apt install docker.io docker-compose
```

Start and enable the Docker service by running:

```
sudo systemctl enable --now docker
```

Verify that Docker is running:

```
sudo systemctl status docker
```

Step 3 

Install Portainer 
We will use Docker to deploy a container with the Portainer container management tool

Run the following command in terminal: 

```
sudo docker volume create portainer_data
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

This command creates a Docker volume named "portainer_data" and then starts the Portainer container, exposing ports 8000 and 9000 for web access. 
The container will be automatically restarted if it crashes or when the system reboots.

You will have to open port 9000 on the instance firewall.

Once the container is running, you can access the Portainer web interface by opening a web browser and navigating to:
http://yourserveripaddress:9000

*You have successfully installed Docker and Portainer on Ubuntu. 
You can now use Portainer to manage your Docker environment.*
