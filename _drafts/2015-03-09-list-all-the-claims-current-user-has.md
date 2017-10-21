---
layout: post
title: List All the Claims Current User Has
date: 2015-03-09 05:02
author: weliwita@gmail.com
comments: true
categories: [Claims, Identity]
---
The easiest way to display All the Claims that were issued to the current user is to query the <a href="https://msdn.microsoft.com/en-us/library/system.security.principal.iprincipal.identity(v=vs.110).aspx" title="Identity">Identity</a> Property of the <a href="https://msdn.microsoft.com/en-us/library/system.security.principal.iprincipal(v=vs.110).aspx" title="IPrincipal">IPrincipal </a>interface.

<pre>
@{
    var identity = (System.Security.Claims.ClaimsIdentity)User.Identity;
}

<ul>
    @foreach (var x in identity.Claims)
    {
        <li> claim:@x.Type -> @x.Value</li>
    }

</ul>

</pre>
