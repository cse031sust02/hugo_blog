---
date: "2017-05-07T16:21:40+06:00"
title: "Say 'Hello' to Node.js"
---

---

## What is Node.js? :
> Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world -- [Official Website](https://nodejs.org/en/)

#### npm?
[npm](https://www.npmjs.com/) is the Node.js package manager. It allows us to easily install modules and packages to use with Node.js.

#### nvm?
[nvm](https://github.com/creationix/nvm/blob/master/README.md) is Node Version Manager. We can install multiple, self-contained versions of Node.js usng nvm. It allows us to control the environment easier (quickly switch to other versions of Node.js).

---

## Installing Node.js
Please visit the [official page](https://nodejs.org/en/download/package-manager/) to install Node.Js in your platform.

To install recent version of Node.js, we will first add a PPA (personal package archive) maintained by [NodeSource](https://github.com/nodesource/distributions)

i.e, To download v6.X
```bash
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Full details can be found [here](https://github.com/nodesource/distributions#installation-instructions)

To verify that the installation was successful, let’s give Node’s **REPL** a try.
```bash
node
>console.log('hello nodejs');
hello world
undefined
> 
```

***REPL** :  REPL (Read-Eval-Print Loop) is an interactive computer programming environment. It takes single user inputs, evaluates them, and returns the result to the user.

> **Q. When i tried to install Node.Js with `apt-get install nodejs` command in Ubuntu 14.04, it installed v0.10.25 instead of the latest version.**

> Ans. Ubuntu 14.04 contains a version of Node.js in its default repositories. The version in the repositories is 0.10.25. This is not be the latest version, but it should be quite stable.

#### install npm?

The nodejs package contains the nodejs binary as well as npm, so we don't need to install npm separately.
But, to run nodejs/npm properly, We may need to install the `build-essentials` package. 

```bash
sudo apt-get install build-essential
```

---

## About npm things  
[npm](https://www.npmjs.com/) is a package manager for javascript. npm makes it easy for JavaScript developers to share and reuse code. Although npm started as the node package manager, but it is now used by almost every popular javascript libraries/frameworks. Please read the [official doc](https://docs.npmjs.com/getting-started) if you want to know more.

#### what is a package?
A package (or sometimes module) contains reusable codes to serve a particular purpose. A package is just a directory with one or more files in it. 

Every package contains a file named **package.json** with some metadata (a short description, GitHub repository etc) about that package.

* Module vs Package :
  A module is anything that can be loaded with require() in a Node.js program. Most npm packages are modules. [more details..](https://docs.npmjs.com/how-npm-works/packages#most-npm-packages-are-modules)

#### npm Registry?
Every time we download a package using npm install, we're downloading it from npm Registry and put in our project's `node_modules` folder. npm Registry is basically a huge database containing each package's files and associated metadata.

#### Initialize a project
npm helps us build projects, but for npm to be able to do that, we need to tell npm a little bit about our project. we have to write the details in **package.json** file.

we can manually create the **package.json** file and write the details. Or we can use 'npm init' command which will ask a bunch of questions, and then it will create the **package.json** for us.

```bash
npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (demo-project) 
```

> the next time we use `npm init` command, it will update the existing **package.json** file.

---

## Dealing with packages

One of the most important things that npm does is install packages.

### Install packages

'npm install' can be used in many ways. By default, `npm install` command (without any arguments) will install all modules listed as dependencies in **package.json** file.

To install a specific package,

```bash
npm install <package>
```
> a **package** can be a folder, a url, a git remote url etc.

> If we install a package with `--save` option, the package will be added to the dependencies list in the package.json file. so, afterwards, running `npm install` will automatically install that package.

We can istall packages **locally** or **globally**

  
- **locally**

By default `npm install` will install modules locally. it downloads the package to 'node_modules' directory. after we installed the package, we can use it in our code.

for exmplae, first install the [lodash](https://lodash.com/) module locally,
```bash
npm install lodash
```

now, we can use in our code,
```javascript
  var lodash = require('lodash');
  var output = lodash.without([1, 2, 3], 1);
  console.log(output);
```

- **globally**

If we want to use any package globally (usually to use it as a command line tool), then we can install those packages globally

for example, install the [forever](https://github.com/foreverjs/forever) package globally.
```bash
sudo npm install forever -g
```

now, we can use this package in our terminal,
```bash
forever start app.js
```

> for permission error, please check https://docs.npmjs.com/getting-started/fixing-npm-permissions

### list of installed packages

To show the installed packages, we can use the `npm list` command.

- **locally** installed packages,

```bash
npm list --depth=0
```
- **globally** installed packages,

```bash
npm list -g --depth=0
```

> we can use 'ls' instead of 'list'.

> depth = depth of the dependency tree.
     
### Update packages

We can update any existing package with `npm update` command

- **locally**

```bash
npm update
```

- **globally**

```bash
npm update -g <package>
```

### Uninstall packages

`npm unistall` command is used to uninstall any package

- **locally**

```bash
npm unistall <package>
```

- **globally**

```bash
npm uninstall -g <package>
```


---

### Useful Links
- **[Official Getting Started Page](https://www.npmjs.com/#getting-started)** 	
- **[NodeSchool](https://nodeschool.io/)**
- **[Stackoverflow post](http://stackoverflow.com/questions/2353818/how-do-i-get-started-with-node-js?rq=1)**
