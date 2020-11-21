---
date: "2017-04-09T16:31:49+06:00"
title: "Blogging with Hugo"
---

## Install Hugo
To install Hugo in your operating system, please visit the [official guide](http://gohugo.io/overview/installing/). As I am using ubuntu, installing Hugo is as simple as `sudo apt install hugo`

## Getting Started

Hugo allows us to scaffold a website quickly and easily.

### create new site

```
$ hugo new site blog
```

### Choose a theme
    
Download a theme from https://themes.gohugo.io/ and put in 'theme' folder

for example, in order to install the [casper](http://themes.gohugo.io/theme/casper/) theme,
```
blog$ mkdir themes
blog$ cd themes
blog/themese$ git clone https://github.com/vjeantet/hugo-theme-casper casper
```
  
### configuration

update your configuration in config.toml

**e.g.,**

```
languageCode = "en-us"
title: "My New Hugo Site"
baseURL = "http://example.org/"

[params]
description = "YOUR DESCRIPTION GOES HERE"
author = "YOUR NAME"
authorlocation = "YOUR LOCATION"
authorwebsite = "YOUR SITE"
bio= "YOUR BIO"

[[menu.main]]
name = "Blog"
weight = -120
identifier = "blog"
url = "/"
```

### create new post

```
$ hugo new post/hello-world.md
```

Now put content inside the newly created hello-world.md file,

**e.g.,**

```
---
date: "2016-04-17T16:12:50+06:30"
title: "Hello world"

---

Hello World. This is my first post.
```

### Serve content

```
$ hugo server -t YOURTHEME
```

As i am using casper theme,
```
$ hugo server -t casper
```

You can view your blog at http://localhost:1313/

*for more details, pleaes visit the [official doc](http://gohugo.io/overview/quickstart/)*

---

## Deploy to Github page

Full details on how to host your Hugo based website on github page can be found here https://gohugo.io/tutorials/github-pages-blog. But if you are a newbie like me, it may will look much complex at first time. So, here are some easy steps...

### Create `(your-project)-hugo` repository

for example, create a new repository in Github named `hugo-blog`.

Now, in your terminal, initialize a new git repo.
```
blog$ git init
blog$ git remote add origin https://github.com/YOURUSERNAME/hugo-blog.git
```

### Create `(your-username).github.io` repository

for example, in my case it is `cse031sust02.github.io`

now, add a submodule with the public folder
```
blog$ git submodule add https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git public

# example
blog$ git submodule add https://github.com/cse031sust02/cse031sust02.github.io.git public
```

### Push Everything to Github

```
blog$ git add .
blog$ git commit -am 'push everything'
blog$ git push -u origin master
```

### Deploy
```
blog$ hugo -t casper
blog$ cd public
blog$ git add .
blog/public$ commit -m "deploy"
blog/public$ push -u origin master
```

Then you should visit the blog at https://(YOUR-USERNAME).github.io. For example, my site is at https://cse031sust02.github.io