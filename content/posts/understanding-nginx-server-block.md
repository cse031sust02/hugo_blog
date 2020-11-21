---
date: "2017-09-19T16:54:45+06:00"
title: "Understanding the Nginx Server Block"
---

We can think of Server Blocks as specifications for individual web sites. Server blocks are the NGINX equivalent of Apache's virtual hosts. So in order to host our websites on Nginx server, we need to understand the directives and settings that make up the server block.

Here is a sample server block configuration :

```
server {
  listen       80;
  server_name  _;

  location / {
    root   /usr/share/nginx/html;
    index  index.html index.htm;
  }

  error_page  404              /404.html;
  location = /404.html {
    root   /usr/share/nginx/html;
  }
}
```

We can see different types of directives such as *listen*, *root*, *server_name*, *location* etc. Let's explore those directives.

### listen
It specifies the IP address / port combination that this server block is designed to respond to.

We can specify **only the port** or **only the address** or **Both**. If a port is omitted, the standard port(80) is used. And if an address is omitted, the server listens on all addresses. We can also use more than one listen directive, if needed. Here are some examples.

**e.g.,** port is omitted :
```
listen     127.0.0.1; 
// will only respond to 127.0.0.1:80
```

**e.g.,** address is omitted :
```
listen     50; 
// will respond to port 50 of all addresses. i.e: 127.0.0.1:50, localhost:50 etc..
```

**e.g.,** IP address / port combination :
```
listen     192.168.25.19:60; 
// will only respond to 192.168.25.19:60
```

### server_name
Nginx also checks the `Host` header of each request. When client makes a requests, Nginx checks if there is any server block that has a server_name directive defined with that "Host". If there is a match, then that server block will responds to that request.

It will be easy to understand with an example.

Let's create two new host in the `/etc/hosts` file :
```
127.0.0.1   localhost
127.0.0.1   www.site-one.com
127.0.0.1   www.site-two.com
```

So, now both **site-one** and **site-two** points to same IP address. But we want to put one website in site-one.com and another website in site-two.com. Let's create two different server blocks for those two hosts :

```
# First Website
server {
  listen       70;
  server_name  www.site-one.com;
  
  root   /usr/share/nginx/html/site-one/;
}

# Second Website
server {
  listen       70;
  server_name  www.site-two.com;

  root   /usr/share/nginx/html/site-two/;
}
```

So now we can access the First Website with the address `www.site-one.com:70`, and the Second Website with `www.site-one.com:70`. Now, there is a Quiz. What website will open when we go to 127.0.0.1:70?

### root

This directive specifies the directory where the website's contents are located. As in our last example, the root directory was `/usr/share/nginx/site-two` for the Second Website. So when user hits the URL *http://www.site-two.com:70/mypage.html*, Nginx will load `mypage.html` file from that directory.

### location

location block is used to decide how to process the request URI (after the domain name or IP address/port). e.g. : 
```
location / {
  # configuration for processing all URIs that do not match other location blocks.
} 

location /one {
  # configuration for processing URIs with '/one'
}

location /two {
  # configuration for processing URIs with '/two'
}
```

A location can be defined either by a prefix string or by a regular expression. The syntax is : 
```
location [modifier] match {
...
}
```

When there is no modifier, the match acts just as a prefix string for the incoming URL. e.g. :
```
location /two {
  # configuration for processing URIs with '/two'
}
```

And when any modifier exists, the way that Nginx matches the location will change.

Here is what different modifiers do :

- = *:* request URI **exactly** matches the location given.
- ~ *:* case-sensitive regular expression match.
- ~* *:* case-insensitive regular expression match.
- ^~ *:* regular expression matching will not take place. 

How nginx performs the matching can be found on their [offcial doc](https://nginx.org/en/docs/http/ngx_http_core_module.html#location). Here is an example for illustrate different types of modifiers :
```
location = / {
    # Only matches the / query.
}

location / {
    # URI beginning with '/'
    # But the process continues searching
}

location /documents/ {
    # URI beginning with /documents/ 
    # But the process continues searching.
}

location ^~ /images/ {
    # URI beginning with /images/
    # The process stops searching
}

location ~* \.(gif|jpg|jpeg)$ {
    # Matches requests ending in gif, jpg or jpeg. 
    # URI beginning with /images/ are NOT handled here
}

```

A more detailed overview of how nginx porcesses a request can be found [here](http://nginx.org/en/docs/http/request_processing.html)