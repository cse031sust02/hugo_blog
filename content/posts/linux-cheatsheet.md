---
date: "2017-05-17T15:50:31+06:00"
title: "Getting Started with Linux Command Line"
---

## What is Linux?

Just like Windows and Mac OS X, Linux is an operating system. It is an open source [Unix-like](https://en.wikipedia.org/wiki/Unix-like) operating system.

Although Linux is generally used to refer to the entire OS, Linux is basically the name of the Kernel which was [developed](https://github.com/torvalds/linux) by [Linus Torvalds](https://github.com/torvalds). I think [this answer](https://unix.stackexchange.com/a/94407) explains it all.

## Linux Commands

We should have some basic ideas of **Shell**, **Bash** and **Terminal** first if we want to work with Linux Command Line.

### Shell 

The shell is a program that takes commands from the keyboard and gives them to the operating system to perform. Linux operating system offers several shells such as : **bash**, **sh**, **csh** etc. Although they have many commands in common, each type has unique features.

- **bash** (Bourne Again SHell) : bash is the default shell for most [Linux distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions). It is an enhanced version of the original Unix shell program.

### Terminal

Terminal (or Terminal Emulator) is a GUI which lets us interact with the shell. So, we can type and execute commands from the Terminal Window. There are many different Terminals bundled with different [Desktop Environments](https://en.wikipedia.org/wiki/Desktop_environment), such as: gnome-terminal (GNOME), konsole(KDE) etc.

---

## Working With the Terminal

We should easily find Terminal from the menu. The Terminal Window is like the image below

![terminal](http://linuxcommand.org/images/Screenshot-Terminal.png "Terminal")

**image source** : [linuxcommand.org](http://linuxcommand.org/images/Screenshot-Terminal.png)

So, when we open the Terminal, we see something like this :
```
username@hostname:~$ 
```

- **username** = the username of the current user.
- **hostname** = name of the computer (to identify on the network).
- **~** = name of the directory you’re in. *`~' refers to user's home directory*
- **$** =  It indicates the end of the shell prompt. if user is logged in as ***root***, then it will show '#' sign instead of the '$' sign. 

#### root

In Linux, the root user is the superuser account. this is a special user account that has permission to do any task on a server. So, logged in as root can be potentially dangerous and we should not do that unless we really have to.

*Still you need to know how do i login as root, right? you should able logged in as root by using the `su -` command on your terminal. If you getting any error message, your root account is likely locked. please check [this tutorial](http://www.wikihow.com/Become-Root-in-Linux) for more information.*	


#### sudo

As we understand, logged in as root can be potentially dangerous and we should try to avoid that. so, how can we execute the restricted commands when needed? the answer is `sudo`. the `sudo` command allows a permitted user to execute a command as the superuser or another user.

for example, if we enter `apt-get update` command in our terminal, we will get the following error,

```
username@hostname:~$ apt-get update
E: Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)
E: Unable to lock directory /var/lib/apt/lists/
E: Could not open lock file /var/lib/dpkg/lock - open (13: Permission denied)
E: Unable to lock the administration directory (/var/lib/dpkg/), are you root?
```

but, when we use `sudo` in that same command, it works perfectly,

```
username@hostname:~$ sudo apt-get update
[sudo] password for username: 
Ign http://dl.google.com stable InRelease
Hit http://packages.microsoft.com stable InRelease                             
Hit http://dl.google.com stable Release.gpg  
........
```

---

## Basic Commands

I think the best site to learn Linux Commands is [linuxcommand.org](http://linuxcommand.org/lc3_lts0060.php). I am just trying to list some basics points.

#### Type of Commands

There are four different kinds of Commands :

- **Executable program** : Any executable program. i.e : `vlc`, `gedit` etc
- **Shell Builtin** : Builtin commands provided by Bash. i.e : `cd`, `type` etc
- **Shell function** : Functions of some commands. 
- **Alias** : alias of any command.

If we want to know the type of any command, we can use the `type` command. i.e, `type cd`


#### Navigation  
- pwd (print working directory)
- cd (change directory) 
- ls (list files and directories)
  - ls -l (in long format)
  - ls -a (including hidden files)

#### Manipulating Files
- cp (copy files and directories)
- mv (move or rename files and directories)
- rm (remove files and directories)
- mkdir (create directories)

> We need to understand [Wildcards](http://linuxcommand.org/lc3_lts0050.php) feature in order to make powerful commands.

#### Current User
- whoami (show user name of current user)
- id (show user and group information)
- groups (groups that current user belongs to)
- passwd (changes password)


#### Permissions
- chmod (modify file access rights)
- chown (change file ownership)

> We should understand [Linux Permissions](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-permissions) clearly.

#### Process
- ps (list of running processes)
- kill (send a signal to processes)

> We should have clear idea about Linux [Processes](http://www.tldp.org/LDP/tlk/kernel/processes.html) and [Job Control](http://linuxcommand.org/lc3_lts0100.php).

---

## Linux Filesystem

It's useful to understand Linux Filesystem. Below is a image to get a basic idea.

![File System](http://i.imgur.com/T6T0sRW.png "File System")

**Image Source** : http://imgur.com/gallery/1DH0O

To know more details, we can visit this [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/pub/fhs-2.3.html) page.


### Useful Links

- [linuxcommand.org](http://linuxcommand.org)
- [howtocode.com.bd](http://sh.howtocode.com.bd) (Bengali)
- [cheatsheetworld.com](http://cheatsheetworld.com/programming/unix-linux-cheat-sheet/)