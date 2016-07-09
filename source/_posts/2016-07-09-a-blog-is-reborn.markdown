---
layout: post
title: "A Blog Is Reborn"
date: 2016-07-09 21:08:33 +0100
comments: true
categories: 
---
Ok, I started off with the best intention of blogging more regularly but 18 months between blog posts was not quite the cadence I was aiming for! Shortly after setting up the blog I rebuild my machine and completely failed in setting up Octopress, following my own steps in ["A Blog Is Born"] just wasn’t working, I was encountering more problems than I knew how to fix I think because most of the tools weren’t playing nicely with each other on Windows so I gave up in a huff until an easy solution came along.
<!--more-->
## Bash on Windows
This year at Build Microsoft announced the ability to run native Bash on Ubuntu on Windows! Apart the obvious advantages of being able to use cmatrix or cowsay I was at first a little indifferent about the announcement until I realised that this might actually mean I could get Octopress working on Windows, so if all goes to plan this will be my fool proof guide to setting up Octopress using Bash in Windows 10.
### Installing Bash
In order to run Bash on Windows you’ll need to be running the Windows 10 Anniversary Update (currently available to Insiders) and then you will need to:
* Turn-on Developer Mode
* Enable the "Windows Subsystem for Linux (beta)" feature

And that’s it, for more information and a more in-depth guide check out https://msdn.microsoft.com/en-us/commandline/wsl/about

### Install the basics
Once you are up and running with bash you’ll need to install the basic tools using apt-get, here’s the list that I used to get started:

* make
* rake
* nodejs
* git
* ruby1.9.1-dev
* bundler

I then pulled down everything from Github and picked up the usual Octopress workflow, and if all goes to plan this should be live within the hour.