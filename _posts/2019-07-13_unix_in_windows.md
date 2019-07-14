---
layout: post
title: Unix in Windows 10
subtitle: Installation of command line tools for Windows 10 users
bigimg: /img/path.jpg
tags: [windows, unix]
---

# Adventures with Unix in Windows 10
 *Author: Chissa Rivaldi
Last Updated: 07/13/2019*
[Link to Intro to Biocomputing tutorial slides from Week 1 Friday](https://docs.google.com/presentation/d/1fK_Y_O_ZVYCWAWh6EXcYmKqcyoP-_EVsrhtOqt6M8cQ/edit?usp=sharing)

---
## Why do we want a terminal on Windows?

Many times you'll run into software that aren't written for Windows. Sometimes your files are too big for your own computer. In these instances, you essentially need a new machine to do your work. You can install something called a [virtual machine](https://medium.freecodecamp.org/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b), which is like putting a mini computer on your computer. These are *really useful* for [some workflows](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4567039/) but they can easily take up a huge amount of space and we don't really need them to accomplish our current objective of simply getting started in UNIX. There are tools like [Binder](https://mybinder.readthedocs.io/en/latest/introduction.html) and [Docker](https://www.docker.com/why-docker) that can be built for specific workflows and make reproducing workflows a breeze, but to get a command line on your local machine, we can get started with something less intensive. 

---

#### First, figure out if you have a 32 or 64 bit operating system. 
Press the windows key and type "about" - select the 'About your PC' option that comes up & look for 'System type' (see example below).  
![](https://i.imgur.com/SqMwFU5.png =500x)


#### Now you can decide out which Unix setup you want to install. 32-bit users, you want Cygwin or MobaXterm. 64-bit users, you can either do a native install of Bash/Ubuntu or install either Cygwin or MobaXterm. (There are other options, but these are the ones I've had the most experience using/installing.)
- Native install of Ubuntu 
    - You'll Windows 10 with 2017 Fall Creator's Update or later -  [Windows update page](https://support.microsoft.com/en-gb/help/4028685/windows-10-get-the-update)
    - [Installation Instructions](https://tutorials.ubuntu.com/tutorial/tutorial-ubuntu-on-windows#0) - [Another Option](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
- MobaXterm ([Website](https://mobaxterm.mobatek.net/download-home-edition.html))

    - [Installation Instructions](https://blog.jez.io/2014/09/28/setting-up-mobaxterm-for-ssh-on-windows/) - Choose Home Edition
    - In my experience, MobaXterm has more bells and whistles, but the tradeoff is that it's a bit slower to load. 
- Cygwin - [Website](http://www.cygwin.com/)
    - Pretty quick and light, make sure you install the tools you might want to use within a terminal (nano, git, python2, curl, wget, unzip, make, and openssh are the ones I chose as per [the class instructions](https://github.com/joneslabND/ICB_Fall2018)).

To test out your install, type 
```ls```
and hit "Enter". This command prints **list** of the files in the directory (a.k.a. foler) you're currently working in. 

A screen like this means you were almost certainly successful: 

![](https://i.imgur.com/6IbCQPQ.png =500x)

What you're seeing in this image is an empty directory - there are no files in this directory yet. You might have some, depending on where you started.

### But I know I have a ton of files on my computer - why can't I see them? 
When you start playing with files on your own computer, you'll notice that the file directory setup you're using isn't the one you're used to (familiar directories like 'Downloads' or 'Desktop' will not be visible). This is because of the way that Unix and Windows interact (i.e. not at all). The way to access your files depends on whether you're using native Ubuntu on Windows or Cygwin or MobaXterm and requires a working knowledge of file paths to understand what's really going on. 

$~$

**Instructions for All Terminals**

If you type `cd` with no arguments and hit "Enter", you'll always go to your default home folder. You can always find out what directory you are currently in by using the command `pwd`:
![](https://i.imgur.com/eipmCWC.png =650x)
$~$

This is similar to what your directory looks like now with a Cygwin setup (bonus: this was the exercise we did in class on Monday!). Some files/directories omitted for clarity. You want to go from your "Default Home" to your "Windows Home" - signified by the blue stars. To get there in this example, you need to go up two directories, then down four; see the red arrows.
$~$
$~$
![file paths](https://i.imgur.com/U4lYc4S.jpg =500x)
$~$
$~$


You can do this all in one step. Here is what that command looks like on my computer (my username is 'criva'):

**For a Cygwin setup**

```criva@Bistromath ~ cd ../../cygdrive/c/Users/criva```

or, alternatively, I could start anywhere on my file system and get to my Windows Home like this:

```crivaldi@Bistromath ~ cd /cygdrive/c/Users/criva```

The difference between these two commands is that in the first, you're using a relative file path, and in the second, you're using an absolute file path. The Software Carpentry lesson on file paths explains this thoroughly if you'd like this broken down in detail.  

$~$

**For Ubuntu on Windows setup**

Relative path: 
```cd ../../mnt/c/criva``` 
or absolute path:
```/mnt/c/criva```

[More info on Ubuntu in Windows 10](https://www.howtogeek.com/261383/how-to-access-your-ubuntu-bash-files-in-windows-and-your-windows-system-drive-in-bash/)

$~$

---

$~$

### Other Tips


   - Explainshell.com is really helpful when you're learning commands (I still use it every now and then tbh)
   - Amazing blog with a lot of comic strip-like information about unix commands. https://jvns.ca/ (cool example: https://jvns.ca/zines/#linux-comics)
   - If, at any point, you need to name something, **do not use spaces**. You can use: '_' or '-' but keep it simple until we learn more about special characters.
    - Use PuTTy, CyberDuck, Rstudio to transport files back and forth (in command line, use the command `scp` is too tricky). 
    - Good text editors with a graphical user interface (GUI) & some fancy tricks:
        - [Sublime](https://www.sublimetext.com/3)
        - [Atom](https://atom.io/)
