---
layout: post
title: "dotnet sln add"
date: 2018-08-17 10:02:03 +0100
comments: true
categories: [dotnet, tips]
---

It's been a while since I'd created a number dotnet projects and supporting solution using the command line so I had to refer to the [documentation](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet) to keep me right. As I had just created a number of projects adding each one to the solution is a little tedious so when I'd spotted I could use [globbing patterns](https://en.wikipedia.org/wiki/Glob_(programming)) I thought this would save time and a few key presses.

<!--more-->

However, when I ran `dotnet sln Foo.sln add **/*.csproj` I was presented with the error `Could not find project or directory **/*.csproj`. It turns out that globbing is not actually supported by the CLI but actually a shell feature and PowerShell wasn't expanding the glob. Luckly as dotnet is cross platform and I have [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) installed with all the dotnet goodness I could switch to `bash`, ensure globbing was enabled using `shopt -s globstar`, and then run `dotnet sln Foo.sln add **/*.csproj` to add all my new projects, job done...
