---
date: "2017-06-20T16:21:21+06:00"
title: "Installing LEMP stack on ubuntu 14.04"
---

---
## What is LEMP stack?

LEMP stands for **Linux**, **nginx** (pronounced engine-x), **MySQL**, and **PHP**. It is actually a variation of the LAMP stack where Apache is replaced with nginx.

---

## Setup 

So, We are going to setup LEMP stack on our ubuntu 14.04 machine.

#### **Step 1 : Update Apt-Get**

Update the package database. To know more about **apt-get**, please visit this [page](https://itsfoss.com/apt-get-linux-guide).

```
sudo apt-get update
```

#### **Step 2 : Install nginx**

Installing nginx is very easy as Ubuntu provides nginx package in its default repositories.

```
sudo apt-get install nginx
```

We should now be able to access the default Nginx landing page from our browser by entering our server's domain name or public IP address.


#### **Step 3 : Install PHP**

Now it's time to install PHP. We will be using PHP 7 which is the latest version. 

First we need to add [PPA for PHP 7](https://launchpad.net/%7Eondrej/+archive/ubuntu/php) to system's Apt sources using [add-apt-repository](http://manpages.ubuntu.com/manpages/trusty/man1/add-apt-repository.1.html) command and then install php and php-fpm packages (since nginx communicates with php-fpm).

```
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.0 php7.0-fpm
```


> We may also need to install modules like php7.0-mysql, php7.0-cli etc based on our application requirements.
```
sudo apt-get install php7.0-mysql php7.0-cli php7.0-mbstring
```
To find out all available PHP7 modules, we can use the `sudo apt-cache search php7-*` command.

###### Configure Nginx to Use the PHP Processor :

Now, we still need to tell nginx to use our PHP processor for serving php files.

First we have to open the default Nginx server block configuration file
```
sudo nano /etc/nginx/sites-available/default
```

There is already a server block there, we will change that with the following code,

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Now, We will restart the nginx server with the following command,

```
sudo service nginx restart
```

We can test if everything is working properly by creating a php file in `/var/www/html` directory and then try to access that file from our browser.

#### **Step 4 : Install MySQL**

Now we will install MySQL. we can do it very easily with the following command,

```
sudo apt-get install mysql-server
```

To verify if MySQL is installed properly, we can try to login

```
mysql -u root -p
```

We should then see a Welcome Screen and we can start writing SQLs there

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 5.7.18-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> 

```