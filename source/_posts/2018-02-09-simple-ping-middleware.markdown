---
layout: post
title: "Simple ping Middleware"
date: 2018-02-09 16:18:39 +0000
comments: true
categories: [HowTo, Tips, dotnet core, ASP.NET, Middleware]
---

If you find yourself needing to create a simple ping endpoint often used by load balancers as a quick check to see if traffic can be directed to your site, rather than complicating the simple and creating an MVC controller etc consider simple middleware.

<!--more-->

The ASP.NET Core request pipeline consists of a sequence of request delegates, these delegates are configured using [Run](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.AspNetCore.Builder.RunExtensions?view=aspnetcore-2.0), [Map](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.AspNetCore.Builder.MapExtensions?view=aspnetcore-2.0) and [Use](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.AspNetCore.Builder.UseExtensions?view=aspnetcore-2.0), and for our simple ping endpoint Map is a perfect fit. Map will create a branch in the pipeline allowing you to break out of the normal flow which could have the advantage as it can keep this as lightweight as you need. The following can be used to return a 200 response to indicate our site should be good to go, if you need to add some health checks or additional logic you could create more complex middleware.


{% codeblock %}
app.Map("/ping",
  ping => ping.Run(async conext => await conext.Response.WriteAsync("ok")));
{% endcodeblock %}

For more information on Middleware check out [ASP.NET Core Middleware](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?tabs=aspnetcore2x#writing-middleware)