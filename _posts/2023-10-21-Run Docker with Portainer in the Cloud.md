---
title: Run Docker with Portainer in the Cloud
date: 2023-10-21
categories: [cloud]
tags: [cloud]
image: /assets/docky.jpg
---


*Docker is a containerization platform that allows you to package 
applications and their dependencies into lightweight, isolated containers. 
These containers can run consistently across different environments, 
making it easier to deploy and manage applications.*


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

![dockerstatus](/assets/dockerstatus.jpg)

Step 3 

Install Portainer 
We will use Docker to deploy a container with the Portainer container management tool

Run the following command in the terminal: 

```
sudo docker volume create portainer_data
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

This command creates a Docker volume named "portainer_data" and then starts the Portainer container, exposing ports 8000 and 9000 for web access. 
The container will be automatically restarted if it crashes or when the system reboots.

Check the status of the docker container created

```
sudo docker ps
```

![dockerps](/assets/dockerps.jpg)

Remember to open port 9000 on the instance firewall.

Once the container is running, you can access the Portainer web interface by opening a web browser and navigating to:
http://yourserveripaddress:9000 

Create your Portainer account 

![createaccount](/assets/createaccount.jpg)

Welcome to the Portainer dashboard 

![portainerdash](/assets/portainerdash.jpg)



*You have successfully installed Docker and Portainer on Ubuntu. 
You can now use Portainer to manage your Docker environment.*

*(We will explore deploying docker images in another article)*
