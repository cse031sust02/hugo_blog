---
date: "2017-08-20T17:18:51+06:00"
title: "How I learned to stop panicking and play with NGINX"
---

---

## What is Nginx
 
Nginx is a high performance web server which is lightweight, free and open-source. It can be used as a standalone [web server](https://youtu.be/XhgUClE5uC0?t=11m13s) (like Apache) or as a [reverse proxy](https://en.wikipedia.org/wiki/Reverse_proxy) (serve in front of the web servers). Nginx is also used as mail proxy server, load balancer and HTTP cache. 

#### Why use Nginx?

There are other web servers such as Apache, IIS etc. So what makes Nginx special? It is especially good at handling many concurrent connections as it was originally developed to handle [C10k problem](http://www.kegel.com/c10k.html) (serving 10000 concurrent connections). Nginx serves requests asynchronously while other web servers (such as Apache, IIS) creates new threads for every request received. 

Nginx can also work alognside other web servers as a reverse proxy. Nginx not only serve HTTP & HTTPS protocol but also IMAP, POP3 and SMPT. We can use Nginx on servers with very limited hardware capabilites. A very detailed overview of why we should use Nginx can be found [here](https://youtu.be/XhgUClE5uC0?t=16m57s).

---

## Installation

There are various ways to download and install Nginx. Please follow [Official Guide](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/) to install Nginx on your system. 

On Ubuntu, One should be able to install Nginx easily with the `apt-get install nginx` command.

After installing Nginx, we should see the welcome page by entering the IP address (we can get that using `ifconfig` command) of our server on a browser.

---

## Configuration

For most linux distributions, all Nginx config files are located in `/etc/nginx` directory. 

**nginx.conf** is the main configuration file. It is Nginx's main control point which reads in all of the other appropriate configuration files and combines them into a monolithic configuration file when the server starts. 

The structure of that configuration file looks like below :
```
user nobody; 

events {
   ...
}

http {
    ...

    server {
    	...
    }

    server {
    	...
    }
}

stream {
   ...
}
```

As we can see, This file consists of **directives** and their parameters. There are two kinds of directives.

- **simple directives** : These directives end with a semicolon.

```
user nobody;
```
- **contexts** : A few directives group together related directives. Those directives are referred to as contexts. i.e, events, http and server etc.

*To know more details about the configuration file and what is the purpose of the each directives, please visit the [official guide](https://www.nginx.com/resources/admin-guide/configuration-files/). This [example](https://www.nginx.com/resources/wiki/start/topics/examples/full/) is helpful too.*

### Hosting Sites

For hosting websites, we need to understand how to set up virtual servers.

A virtual server is defined by a server directive in the http context.

```
http {
    server {
        # Server configuration
    }
}
```

And it is possible to add multiple virtual servers into the http context. 
```
http {
    server {
        # Server One configuration
    }

    server {
        # Server Two configuration
    }
}
```

Now, if we add 10 virtual servers, the **nginx.conf** file will become very long and modifying that file will be a headache. This is why **sites-enabled** folder exists. We can make seperate configuration file for each virtual host. And in the main nginx.conf file, we will include that folder :
```
http {
    # Virtual Hosts
    include /etc/nginx/sites-enabled/*;
}
```

So, now every virtual servers listed in **sites-enabled** folder will be public to visitors.

We usually have to manage many different sites and may need to activate/deactivate any particular site anytime. This is why we use **sites-available** folder for storing all of our virtual host configurations(whether they're currently enabled or not). To enable any particular virtual host, we will symbolically link it's configuration file to **sites-enabled** directory.

I have written another [post](https://cse031sust02.github.io/post/understanding-nginx-server-block/) where i tried to explain the server block in details.

---

## Reloading Nginx

Whenever we change the configuration, we will need to restart nginx server for changes to take place.
```
sudo service nginx restart
```
