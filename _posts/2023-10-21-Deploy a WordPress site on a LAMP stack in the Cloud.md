---
title: Deploy a WordPress site on a LAMP stack in the Cloud
date: 2023-10-21
categories: [cloud]
tags: [cloud]
---

![WordPress](/assets/wordpress.png)


*WordPress is one of the most popular content management systems and today we will deploy this famous open-source 
program on our very own cloud instance*

First, create your virtual cloud instance. I will be making use of Ubuntu on xneelo.

Create an instance: How to guides

<a href="https://xneelo.co.za/help-centre/cloud/create-an-instance" target="_blank">xneelo Cloud </a>  
<a href="https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html" target="_blank">AWS EC2 </a>  
  <a href="https://cloud.google.com/compute/docs/instances/create-start-instance" target="_blank">MS Azure VM </a>


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

Start and enable Apache

```
sudo systemctl start apache2
sudo systemctl enable apache2
```

Step 3 

Install MariaDB database server 

```
sudo apt install mariadb-server
```

Secure the database (Follow the instructions after running the command)

```
sudo mysql_secure_installation
```

Copy the following code into a file 

Create the file

```
sudo nano adduser.sh
```

Paste the below code in the file and save the file by pressing *Ctrl + x*, *Y* & *Enter*

```
#!/bin/bash

# Prompt the user for database details
read -p "Enter the desired database name: " db_name
read -p "Enter the desired username: " username
read -s -p "Enter the desired password: " password
echo

# Access the MariaDB server
mysql -u root -p <<EOF
# Create the database
CREATE DATABASE $db_name;

# Create the user and set the password
CREATE USER '$username'@'localhost' IDENTIFIED BY '$password';

# Grant privileges to the user on the database
GRANT ALL PRIVILEGES ON $db_name.* TO '$username'@'localhost';

# Flush privileges
FLUSH PRIVILEGES;

EOF

# Inform the user about the success
echo "Database, username, and password created successfully."
```

Run the script and setup your database credentials 

```
sudo bash adduser.sh
```

Step 4

Install PHP

```
sudo apt install php libapache2-mod-php php-mysql
```

Step 5

Navigate to the *html* directory

```
cd /var/www/html
```

Download and install WordPress

```
sudo wget https://wordpress.org/latest.tar.gz
```

Unpack the Tar file 

```
sudo tar -xzvf latest.tar.gz
```

Move the WordPress files

```
sudo mv wordpress/* .
```

Remove the empty directory

```
sudo rmdir wordpress
```

Set the permissions 

```
sudo chown -R www-data:www-data /var/www/html/
```

Copy the WP-Config file

```
cp wp-config-sample.php wp-config.php
```

Configure the wp-config file with the MySQL database credentials 

```
sudo nano wp-config.php
```
Update the lines as indicated below:

```
define('DB_NAME', 'yourdbname');
define('DB_USER', 'yourdbuser');
define('DB_PASSWORD', 'yourdbpassword');
```

*Complete the installation*

Open your web browser of choice and navigate to your instance IP address. 
The WordPress installation wizard should appear.

You can follow the on-screen instructions to complete the installation


