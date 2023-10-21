---
title: "Deploy a WordPress site on a LAMP stack in the Cloud"
date: 2023-10-21
categories: [cloud]
tags: [cloud] [wordpress] [LAMP]
---

# Deploy a WordPress site on a LAMP stack in the Cloud


WordPress is one of the most popular content management systems and today we will deploy this famous opens source 
program on our very own cloud instance

Step 1
Spin up your virtual cloud instance. You can use any platform such as AWS, Azure or Google Cloud. 
I will be making use of the xneelo Cloud instance running Ubuntu Linux 

Step 2 
Update the OS repositories

````
```
sudo apt update 
```
````


sudo apt upgrade

Step 3 
Install Apache 

```sudo apt install apache2```
