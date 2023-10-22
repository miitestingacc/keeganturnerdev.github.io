---
title: Deploy a WordPress site on a LAMP stack in the Cloud
date: 2023-10-21
categories: [cloud]
tags: [cloud]
---

![WordPress](/assets/wordpress.png)


WordPress is one of the most popular content management systems and today we will deploy this famous opens source 
program on our very own cloud instance
Create your virtual cloud instance. You can use any platform such as AWS, Azure, or Google Cloud. 
I will be making use of the xneelo Cloud instance running Ubuntu Linux

Step 1

Update repositories

```
sudo apt update -y
```

```
sudo apt upgrade -y
```


Step 2

Install Apache web server 

```
sudo apt install apache2
```
