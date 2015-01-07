---
layout: post
title: "TFVC and NuGet Updates"
date: 2015-01-07 12:00:04 +0000
comments: true
categories: 
---
At some point, for no obvious reason, I kept encountering an error when updating some NuGet packages, the error (TF14092) was basically telling me a file could not be modified as there was a pending delete. Experience has taught me that there is generally a reason for sudden changes in behaviour and after a little analysis I eventually worked it out.
<!--more-->
We currently use TFS2013 for version control, our main solution uses Visual Studio 2013 and we rely on a number of packages from [NuGet](http://www.nuget.org/) as well as an internal repository for internal or licensed 3rd libraries. Historicity this has not always been the case, we've upgraded the solution through various versions of Visual Studio and TFS has also been upgraded from TFS2010, but the occurrence of this problem didn't appear to tie in with either upgrade. What I eventually worked out was that I had been using a server workspace long after the primary project had been upgraded, it wasn't until I was free of some of our older projects that I upgraded to a [local workspace](http://msdn.microsoft.com/en-us/library/bb892960.aspx) that had actually introduced this behaviour.

Once I realised the root cause the solution was simple, I created a new workspace on my PC but ensured it was a server workspace, opened the solution from this workspace and upgraded my NuGet packages, I could have alternatively changed the existing workspace from local to server but I think local workspaces work better for me.
 
For future reference the full error is:
{% codeblock %}
1 error(s) encountered attempting to perform the add operation on 1 item(s) First error encountered:
TF14092: The item $/SOMEITEM cannot be changed. A parent of this item has a pending delete which must be checked in first.
See output tool window for information on any other errors.
{% endcodeblock %}