---
layout: post
title: List All the Claims of the Current User
date: 2015-03-09 05:02
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, IAM]
tags: [claims]
---
The easiest way to display all the claims that was issued to the current user is to query the <a href="https://msdn.microsoft.com/en-us/library/system.security.principal.iprincipal.identity(v=vs.110).aspx" title="Identity">Identity</a> property of the <a href="https://msdn.microsoft.com/en-us/library/system.security.principal.iprincipal(v=vs.110).aspx" title="IPrincipal">IPrincipal </a>interface.

Here is the sample code in razor view.
{% highlight csharp %}
@{
    var identity = (System.Security.Claims.ClaimsIdentity)User.Identity;
}

<ul>
    @foreach (var x in identity.Claims)
    {
        <li> claim:@x.Type -> @x.Value</li>
    }

</ul>

{% endhighlight %}
