---
date: "2017-04-23T17:37:13+06:00"
title: "Getting Started with Composer"
---

## What is [Composer](https://getcomposer.org/)?
> Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you. 

> **source** : [getcomposer.org](https://getcomposer.org/doc/00-intro.md) 


### Why Use Composer?
Suppose, we want to use a mail library for our PHP project, let's say [PHPMailer](https://github.com/PHPMailer/PHPMailer). We would normally download the PHPMailer library and put it on our project's folder. But, PHPMailer depends on some other libraries too. So we need to download those libraries too. Now, those libraries depends on other libraries and the list goes on. This is where Composer comes in, It enables us to declare the libraries our project depends on. And Composer will handle the dependency resolution automatically. So, when we install PHPMailer using Composer, it will pull in all the required libraries, dependencies and manage them all in one place.

*This kind of concept is not new, and in fact, Composer is strongly inspired by node's [npm](https://www.npmjs.com/) and ruby's [bundler](http://bundler.io/).*

Another benefit of using composer is avoid the pain of autloading. As we have all many different packages in our project, we need the ability to autoload them into our project. For libraries that specify autoload information, Composer generates a 'vendor/autoload.php' file. We can simply include this file and start using the classes that those libraries provide without any extra work.

Composer is used in all modern PHP frameworks (Symfony, Laravel etc).

---

## Using Composer
Now, let's start using composer. 

### Installation
Composer requires PHP 5.3.2+ to run. To install composer on your system, just follow the [official guide](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx)

### Some useful commands

- list of available commands and description :

```bash
composer
```

- check current version 

```bash
composer -V
```

- update to the latest version

```bash
composer self-update
```

- get help for that command

```bash
composer help [command-name]
``` 

- check for common problems.

```bash
composer diagnose
``` 


## Project Setup

To start using Composer in our project, all we need is a `composer.json` file. This file describes the dependencies of our project (and may contain other metadata as well).

For example, if we want to use [PHPMailer](https://packagist.org/packages/phpmailer/phpmailer) and [Monolog](https://packagist.org/packages/monolog/monolog), we can create the following composer.json file.

```php
{
    "require": {
        "phpmailer/phpmailer": "~5.2",
        "monolog/monolog": "*"
    }
}
```

For more information about `composer.json` file, please see the [composer documentation](https://getcomposer.org/doc/01-basic-usage.md#composer-json-project-setup). We also need to have a clear idea about [versions](https://getcomposer.org/doc/articles/versions.md). 


### Install Dependencies
Then we can install the dependencies for our project simply with a `composer install` command.

This will automatically download the dependencies into our project under the directory 'vendor'.

### Start using those Dependencies
As stated before, Composer generates a 'vendor/autoload.php' file. So, we can just include that file and start using the classes the installed libraries provide. for example : 
```php
require __DIR__ . '/vendor/autoload.php';

$log = new Monolog\Logger('name');
$log->pushHandler(new Monolog\Handler\StreamHandler('app.log', Monolog\Logger::WARNING));
$log->addWarning('Foo');
```

### Update Dependencies

Whenever we want to update our dependencies to latest versions, we can use this command `composer update`.

To update any single package only, the command will be : `composer update [package-name]`

---

## Did you know?
We have to understand few key facts while working with composer

### # 'composer install' vs 'composer update'
To get a clear idea what actually happens when we use the `composer install` & `composer update` commands, please visit the [official doc](https://getcomposer.org/doc/01-basic-usage.md#installing-dependencies). I am trying to write the thing in my own way.

if we run `composer install` for the first time in our project, 

  - Composer will download the dependencies (with defined versions) listed in **composer.json** file. 
  - After installation is complete, Composer will create a file named **composer.lock** to store information of all the downloaded packages and their versions.

From next time, whenever we run `composer install` command, Composer will download the dependencies listed on **composer.json**, But it will use the *exact versions* listed in **composer.lock** file. 

So, if we change the **composer.json** file (ie, add new package, chage version of any package etc) and then try to run the command `composer install` command, it will show an warning.
```bash
Warning: The lock file is not up to date with the latest changes in composer.json. You may be getting outdated dependencies. Run update to update them.
```

So in that case, we have to use `composer update` command. `composer update` command fetches the latest matching versions (according to our **composer.json** file) and update the composer.lock file with the new versions. This is equivalent to deleting the composer.lock file and running install again.

So, we should only ever run `composer update` to get the newest versions of our dependencies, not to install them.

### # install with `composer require` Command
In our example, We could define and install dependencies with a single [`composer require`](https://getcomposer.org/doc/03-cli.md#require) command.

for example :

```bash
composer require phpmailer/phpmailer:5~5.2 monolog/monolog:*
```

when we run `composer require` command,

- it adds new packages to the composer.json (If composer.json file does'nt exists, it will create one)
- the modified requirements will be installed or updated.

