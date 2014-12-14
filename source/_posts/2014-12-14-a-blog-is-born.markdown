---
layout: post
title: "A Blog Is Born"
date: 2014-12-14 11:23:47 +0000
comments: true
categories: 
---
So I've decided to start a blog, not for the first time, I've had a few attempts on a couple of different platforms from a custom web app to [Umbraco](http://umbraco.com/) and I've probably got stuff on Geeks with Blogs and Blogger too. This time I'm going for an Octopress and GitHub Pages combo and I know little of either! Thankfully both are fairly well documented and hopefully be able to learn a few things along the way.

This first post will hopefully detail how to get started, **[SPOILER ALERT]** I guess if you are reading this then this has proven to be successful. I'm using my trusty Surface Pro running Windows 10 Tech Preview so a good starting point looks to be [How to Install and Use Octopress on Windows](http://thaiat.github.io/blog/2014/03/13/how-to-install-and-use-octopress-on-windows/) so let's see how this goes.
## 1. Getting the basics installed
To get started we'll need a couple of things installed and [Chocolatey](https://chocolatey.org) is the best place to start this process! Once installed (or updated in my case) the following packages should be installed:

* `choco install git`
* `choco install ruby -version 1.9.3.54500`
* `choco install ruby.devkit`
* `choco install python`

## 2. Install Octopress
Once everything is installed and the command prompt is restarted lets get Octopress installed, configured and deployed.

* `git init`
* `git clone git://github.com/imathis/octopress.git nyami.github.io`
* `cd nyami.github.io`
* `gem install bundler`
* `bundle install`
* `rake install`
* `notepad .\_config.yml` and update properties and save
* `echo www.nyami.uk >> source/CNAME`
* `rake new_post["A Blog Is Born"]`
* `rake generate`
* `rake preview`
* `rake setup_github_pages[https://github.com/Nyami/nyami.github.io.git]`

at this point I got the following error:

{% codeblock %}
## Set the codepage to 65001 for Windows machines
** Invoke setup_github_pages (first_time)
** Execute setup_github_pages
rake aborted!
ArgumentError: invalid byte sequence in UTF-8
C:/GitHub/nyami.github.io/Rakefile:393:in `strip'
C:/GitHub/nyami.github.io/Rakefile:393:in `blog_url'
C:/GitHub/nyami.github.io/Rakefile:344:in `block in <top (required)>'
{% endcodeblock %}

using the command `chcp 65001` at this point didn't help so I had a quick peek at "Rakefile" not really knowing what it is but the problem looked to be around the CNAME file created above so I changed the encoding to ANSI and tried again and this time it was successful.
 
Now I'm going to try get this up on Github... lets see what happens... 

**Update** 
So looks like everything worked using the following workflow:

* `git add .`
* `git commit -m "first commit of Octopress blog"`
* `rake deploy`
* `git push origin source`

This was surprisingly easy, hopefully over the next few months I'll get some new posts up...
