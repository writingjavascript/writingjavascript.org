---
title: Node.js Development Environments for Beginners
contributors: [sethvincent]
topics: [git, node, atom, terminal, budo, npm]
description: "Learn to set up a development environment for JavaScript & Node"
updated: "January 3, 2017"
---

# Setting up a development environment for JavaScript & Node

> This guide is a work in progress! [Suggest changes or make contributions](/contributing) and [find out when we release updates](/newsletter).

Before starting a project, we must make sure our development environment is ready. This can be daunting when getting started programming, so we'll try to go through it in a very detailed way.

But remember: changes you make can be reverted, issues you face can be solved. It sometimes takes patience & stubborn determination to get a computer to do what you want, but you're capable, and there are folks who are willing to help.

For instance, there are a few places where you can ask for help with blockers like setting up development environments. For a list of those, read the [learning communities topic page](/learning-communities).

## What is an environment?

An environment is a set of conditions under which you will create your project. When we work on and run a project on a personal computer during development, that's a **development environment**. When we launch a project so it is running on an external server and is available to users, that's a **production environment**.

It's common to also set up a private **staging environment** where you can review changes on an external server that is identical to the production environment to help check the quality of the changes before making them public. With some projects it can also be useful to create **test environments** that are dedicated to testing code, often with configuration & conditions to test & debug specific problems or potential issues in the code.

For this guide, we'll be focusing just on development environments.

## What is a development environment?

A development environment is a collection of libraries & tools needed to work on a project. A programmer needs a set of tools and materials the same way a woodworker does. Our tools are digital and focused on code. Our materials are the code that we use as dependencies.

## What is a dependency?

A dependency is a specific tool or library that we need to complete our work.

There are a few types of dependencies:

- project-specific dependencies
- development dependencies
- system dependencies

### System dependencies

These are the foundational dependencies that are required before even getting started developing a project.

### Development dependencies

These are project-specific development tools used to test, create builds, and perform other tasks related to creating a project.

### Project-specific dependencies

These are the modules, the libraries, the little bits of code that make your project function. These are most commonly just referred to as dependencies. Any time in these docs you see a reference to a "dependency" without the label of "system" or "development", know that we're referring to these project-specific dependencies. For our purposes this might include JavaScript, CSS, HTML, fonts, images, or potentially other types of dependencies.

## Getting started

We're focused on JavaScript, Node, and related tools, so that informs the types of dependencies we'll be focusing on as we set up our development environment.

## Installing system dependencies

There are three primary system dependencies that we'll be using:

- [Node](/node)
- [Git](/git)
- [Atom](/atom)

Before we install those, however, there are a few dependencies specific to the operating system that you're using that must be installed.

### MacOS

Before installing other system dependencies, you'll need to install the macOS command-line tools. These instructions work for macOS 10.9 and newer.

In the terminal application, run this command:

```
xcode-select --install
```

A popup will ask for confirmation to install the tools.

### Windows

On Windows, you may find that you need an alternative terminal application in place of Powershell or cmd.exe.

On Windows 10, we recommend installing the new Bash for Windows. 

We also recommend the terminal emulators [hyper](https://hyper.is) and [cmder](http://cmder.net).

### Linux

You may need to install lower-level system dependencies. On Ubuntu for instance, you may need to use `apt-get` to install these packages:

```
sudo apt-get install build-essential libssl-dev
```

### Installing Node

For the quick and easy Node install process, go to [nodejs.org](http://nodejs.org) and download the latest version for your operating system.

You'll download an installer program that walks you through installation.

For more detailed info about Node installation, including a solution that lets you install multiple versions of Node, see the [Node topic page](/node)

### Installing Git

Similarly, you can download git from the [git website](https://git-scm.com/)

After downloading, run the installer program it will walk you through installation.

There is more detailed information about installing and using git in the [git topic page](/git).

### Installing Atom

Download atom from the [atom website](https://atom.io).

After downloading, run the installer program it will walk you through installation.

There is more detailed information about using atom in the [git topic page](/atom).

### Make sure system dependencies are set up

Check that Node is properly installed by running the `node` command:

```
node --verson
```

This should print the version of Node that's currently installed and active on your computer.

Check that Git is installed by running the `git` command:

```
git --version
```

This should print the version of Git that's currently installed and active on your computer.

## Setting up an example project

To practice with setting up a development environment, and make sure system dependencies are set up correctly, let's create an example project.

The first step to creating the example project is using the terminal to create a directory on your computer.

If you're new to using the terminal, check out the [terminal topic page](/terminal) to get acquainted. You should particularly look at the terminal doc for notes on getting started on your specific operating system. For example, we use linux/unix commands, and have a few suggestions on what you can do on Windows to be able to use the same set of commands.

### Create a directory

To get started with our example project, we'll:

1. Open the terminal application
2. Create a directory with the `mkdir` command in the terminal.

#### 1. Open the terminal application

On Mac, you'll open `Terminal` from the `Applications` directory.

On Linux, you probably already know where it is 😃.

On Windows, open your linux-like terminal application of choice. On Windows 10, we recommend installing the new Bash for Windows. We also recommend [cmder](http://cmder.net), a terminal emulator.

#### 2. Create project directory

We're going to create the example-project directory inside your home directory.

#### What is the home directory?

The home directory is an area allotted to your user on the computer.

In most cases, when you open your terminal app it will by default put you in your home directory.

To quickly navigate to your home directory you can use the `cd` command:

```
cd ~
```

The tilde, `~`, is an alias to your home directory.

You can see if you are inside your home directory using the `pwd` command.

Run `pwd` in your terminal. It will print the directory that you are currently in. In my case, the terminal prints:

```
/Users/sdv
```

That's my home directory!

We can double check by running the `~` alias in my terminal by itself. Just type `~` in your terminal app and press **return**.

In my case, when I run `~` I see:

```
-bash: /Users/sdv: is a directory
```

Great! It looks like I'm definitely inside my home directory.

#### Create the directory

First we'll create a `projects` directory in your home directory, then create the `example-project` directory inside of there.

Create the `projects` directory:

```
mkdir projects
```

Change directory into `projects` using the `cd` command:

```
cd projects
```

Create the `example-project` directory:

```
mkdir example-project
```

Change directory into `example-project` using the `cd` command:

```
cd example-project
```

> Tip: to create both directories at once, we can use the `-p` command with `mkdir`: `mkdir -p projects/example-project`

## Using the `npm` command

When we installed Node, the `npm` command was installed along with it.

npm is a registry for packages of code, and a command-line tool for installing, publishing, and working with packages of code in various ways. Learn more about npm at the [npm topic page](/npm).

In this section we'll use the `npm init` and `npm install` commands.

`npm init` creates a `package.json` file where we are able to define the dependencies, development dependencies, and other metadata about our projects.

`npm install` installs dependencies from the npm registry.

You can install regular project dependencies with `npm install --save {package-name}`

Install development dependencies with `npm install --save-dev {package-name}`

The `--save` and `--save-dev` options will list the package in the `dependencies` and `devDependencies` lists in your project's package.json file.

### Run the `npm init` command

To create your project's package.json file, run `npm init` in your terminal.

You'll be prompted to provide information that will be used to fill out the metadata of the package.json file.

Each of these items will prompt you to enter text:

```
name: (example-project) 
version: (1.0.0) 
description: a project for learning about development environments
entry point: (index.js) 
test command: 
git repository: writingjavascript/example-project
keywords: 
author: sethvincent
license: (ISC) 
```

For most of these you can press **Return** to use the default value. When you're finished it'll show you the file it is about to write. In my case it looked like this:

```
{
  "name": "example-project",
  "version": "1.0.0",
  "description": "a project for learning about development environments",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/writingjavascript/example-project.git"
  },
  "author": "sethvincent",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/writingjavascript/example-project/issues"
  },
  "homepage": "https://github.com/writingjavascript/example-project#readme"
}
```

Hit **Return** again to confirm that this is correct.

## Initialize git with `git init`

Similar to the `npm init` command, we're going to initialize our git repository for this project with the `git init` command.

Go ahead and run that now:

```
git init
```

This creates a `.git` directory inside your example-project directory with all the version data and config for git to function.

### More about git

Read more about using git in the [git topic page](/git).

## Using npm scripts

Inside your package.json file there's a section that looks like this:

```json
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
},
```

The `scripts` object in a package.json file defines tasks that can be run as part of developing a project.

You might have a script that creates a build of your project, that tests your code, that runs a development server, or other tasks.

Let's rewrite our scripts object to add an `example` script. In that script we will use the `echo` command similar to as seen in the existing `test` script.

Rewrite your scripts object so it looks like this:

```json
"scripts": {
  "example": "echo \"this is an example\""
},
```

Now you can run the `example` command using `npm run`:

```
npm run example
```

You should see output similar to the following:

```
> example-project@1.0.0 example /Users/sdv/projects/example-project
> echo "this is an example"

this is an example
```

We'll use npm scripts often to create scripts that run the various development dependencies that help to automate tasks and make it easier to work on the project.

## Creating a JavaScript file

We need a place to put some example JavaScript code, so let's create a file named `index.js`.

Naming the main file in a project `index.js` is a convention in Node & JavaScript.

You can use the `touch` command to create a file if it doesn't already exist:

```
touch index.js
```

## Installing development dependencies

We're going to use the `npm` command to install the development dependencies for your example project.

Let's install a development server named `budo`. Learn more about budo in the [budo topic page](/budo).

### Install budo using the `npm install` command:

```
npm install --save-dev budo
```

Let's now create an npm script for running budo.

In the `scripts` object of the package.json file, add a `start` script.

The content of the `start` script will be `budo index.js`.

After adding the `start` script your `scripts` object should look like this:

```json
"scripts": {
  "example": "echo \"this is an example\"",
  "start": "budo index.js"
},
```

Great! We've got a development server set up!

## Running the example project locally

Now that we have a `start` script set up we can use it to run our development server.

Run the command in your terminal:

```
npm start
```

You should see output similar to this:

```
> example-project@1.0.0 start /Users/sdv/projects/example-project
> budo index.js

[0001] info  Server running at http://10.230.148.170:9966/ (connect)
[0001] 97ms       1398B (browserify)
```

This is great! It's working.

## Commit your work

Let's save our work so far using git.

To do that, there are two commands that we'll run: `git add` and `git commit`. Don't run the commands yet, we'll go over them in more detail first.

We will run `git add` to tell git which files we'd like to commit. This is like adding them to a staging area in preparation for being fully saved. We can run `git add {some-file-name}` to add a specific file, or we can run `git add --all` to add all the files in a directory.

We will run `git commit` to fully save the files, and we add a message to the commit to describe the changes we made.

Before we run those commands, let's create a **.gitignore** file that is used to tell git to never include certain files in the version history.

You can create a file through Atom, by right-clicking on the example-project directory, choosing **New file**, and naming it .gitignore or you can run `touch .gitignore` in the terminal.

Add the following to the .gitignore file:

```
node_modules
```

If you're using macOS, you may also want to add `.DS_Store`, an obnoxious little file that tracks custom attributes in a macOS folder. It never should be checked in to git.

Now that we've got the .gitignore file, let's add some files with `git add`.

Because we have a .gitignore file telling git to ignore files we don't need, let's add all the files in the example-project directory:

```
git add --all
```

Now let's create a commit:

```
git commit -m "Set up project"
```

Note that the `-m` and the text in quotes is the message we're using to describe the commit. It's important to be brief & clear about the changes.

It helps to make a small amount of changes in each commit, or limit the types of changes in a commit.

For instance, I might make a commit that fixes typos in a docs page in one commit. Or refactor a function in another commit.

If you're making a lot of different types of changes before making a commit you should consider slowing down and tracking each change carefully with commits.

It's like saving a text document in an editor like Word. Save often.

With git commits we expand that rule: save often and clearly describe your changes.

## Storing your work online

Interested in storing your code online? You might do this to back up your work, publish your work so others can use it, or to collaborate with others on the project you're building.

[GitHub](https://github.com) is a popular choice for hosting code.

You should also check out [GitLab](https://gitlab.com). They let users have free private repositories. I know that when I started learning to code I wished for free private git hosting so I could experiment in private. If that's what you're looking for GitLab is a good choice.

## What's next

In the next section we'll go into depth with using the terminal, git, and atom.

The next section isn't released yet. Sign up for our newsletter to find out when it's published:

{% include newsletter.html %}
