---
title: Build your own storage server with NextCloud
date: 2023-10-21
categories: [cloud]
tags: [cloud]
image: /assets/nxtc.png
---

*Nextcloud is an open-source cloud platform that allows you to store, sync, and share files, calendars, contacts, and more. It provides secure and self-hosted cloud storage solutions, allowing you to have control over your data and privacy.*

For this installation, I will be using Ubuntu as my distribution of choice. 
The below commands will work on any Debian-based distribution.

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

Run the script and set your database credentials 

```
sudo bash adduser.sh
```

Step 4

Install PHP

```
sudo apt install php libapache2-mod-php php-mysql
```

Step 5

Download Nextcloud

```
wget https://download.nextcloud.com/server/releases/latest.tar.bz2
```

Extract the downloaded file and copy the file contents to the html directory

```
tar -xvjf latest.tar.bz2
```

```
sudo copy -r nextcloud/* /var/www/html/
```

Set the correct permissions 

```
sudo chown -R www-data:www-data /var/www/html/
```

Open a web browser and navigate to your server's IP address
Follow the on-screen instructions to complete the Nextcloud installation.
Create an admin account and specify the MySQL database details you set in step 3.





