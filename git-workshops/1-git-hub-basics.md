# Github Basics

Commands always go in the Terminal. your code for the project goes into the files.

1. [Visualization and Resources](#1-visualization-and-resources)
2. [always know where you are!!!](#2-always-know-where-you-are!!!)
3. [VS Code sidebar](#3-vs-code-sidebar)
4. [THE COMMANDS](#4-the-commands)

   a. [pull](#a-pull)

   b. [update file](#b-update-file)

   c. [add](#c-add)

   d. [commit](#d-commit)

   e. [push](#e-push)

## 1. Visualization and Resources

For visualalization of the following steps I find this [article](https://rachelcarmena.github.io/2018/12/12/how-to-teach-git.html) really helpful.
Also super helpful is the following[ tool](http://git-school.github.io/visualizing-git/#free) to just enter all commands you might imagine just to see what will happen.
So just get used to everytime you start working the frist thing you do is :

For setting up your branch to the remote and pushing [this](http://git-school.github.io/visualizing-git/#upstream-changes) version of the tool is super helpful.

## 2. always know where you are!!!

First you will open a terminal in your VS Code. Then navigate to the `dlt-dev-NFT-project`. As the github project is set up in this directory please be sure that you are there when excecuting git commands.
if you do it somewhere else nothing will happen. Or depening on the command you will mess up your gitSetup and will have to do it again.. But also feel free to try it out.

![sidebar](./Bildschirmfoto%202021-08-03%20um%2021.25.14.png)

## 3. VS Code sidebar

on the sidebar you will see several symbols. Hover over them and find out what they mean. the one you see in the image with the blue one is your source control icon. Here you can always see how many files you have changed. If it is loading and doesn't stop, you are either not logged in, or you maybe just set up a git project inside of a git project.
If you are not logged in you will see an info about that in the bottom of your VS Code.

## 4. THE COMMANDS

a. [pull](#a-pull)

b. [update file](#b-update-file)

c. [add](#c-add)

d. [commit](#d-commit)

e. [push](#e-push)

Before starting to work on a file make sure you have the latest version of the project on your local machine.
This can be done by just entering the follwoing command in the command line in the terminal.

### a. pull

```
git pull
```

### b. update file

Okay. Next step is to update a File.
The first thing we ask you to do is adding your name to the README.md file and also add your name to any team you would like to join.
The `README.md`file is written in Markdown. And to see how it will look compiled, you can just do right click with your mouse and select `Open Preview`or if you are inside of the file just press `Cmd + Enter + V`.

So far so great. **Save the file** and now it's the next step.

### c. add

the next command that you will enter in the command line is

```
git add -A
```

this means that you are staging all your changes

### d. commit

then you want to commit these changes to your local repository. When commiting you should always add a commit message. This is important when you or other people want to retrace your changes or only apply some changes.
As a message you would normally just describe what you did in imperative

So when you added your name to the file, you would write `Add name YOUR_NAME to README.md`. Other commands could start with `Fix bug XY`or `Remove unsed code`.

When working on a project you normaly also write the number of the issue or ticket you are working on in the front, like `#15 create tutorial to set up a gitHub project`.

```
git commit -m"#15 create tutorial to set up a gitHub project"

```

### e. push

Now you have the changes stored in your local repository you want to add these changes to the remote repository so other people can see them.

for that you just enter in the command line

```
git push
```
