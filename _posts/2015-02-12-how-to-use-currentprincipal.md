---
layout: post
title: How to Use CurrentPrincipal
date: 2015-02-12 05:48
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, Identity and Access Management]
tags: [authentication, claims]
---

The user running a .Net application is identified by the `Thread.CurrentPrincipal` property of the running thread. You can set the `CurrentPrincipal` at application startup as follows.

{% highlight csharp %}
string[] roles = { "Manager", "Administrator" };
Thread.CurrentPrincipal = new GenericPrincipal(
new GenericIdentity("John"), roles);
{% endhighlight %}

Then later you can make authorization decisions based on the current user.

{% highlight csharp %}
if (!System.Threading.Thread.CurrentPrincipal.IsInRole("Manager"))
{
    Console.WriteLine("Permission denied");
    return;
}
else{
    Console.WriteLine("Permission granted");
    return;
}
{% endhighlight %}

### References

<a title="msdn documentation" href="https://msdn.microsoft.com/en-us/library/system.threading.thread.currentprincipal(v=vs.110).aspx">msdn documentation</a>
