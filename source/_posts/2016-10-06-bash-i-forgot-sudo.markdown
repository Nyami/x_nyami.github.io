---
layout: post
title: "Bash - I forgot sudo"
date: 2016-10-06 09:16:59 +0100
comments: true
categories: 
---

If you’re new to running Bash on Windows like me chances are you’ll type some huge long command only to be presented with a nice message telling you that permission was denied and then you realise you forgot “sudo”. Rather than typing the whole thing again prefixing with sudo this handy alias will save you a few keystrokes:

- Edit bashrc (vi .bashrc)
- Add the alias “ffs='sudo $(history -p !!)'”
- Restart/open bash console

And in case you struggle with vi here is a handy [cheat sheet](http://www.lagmonster.org/docs/vi.html).
