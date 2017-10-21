---
layout: post
title: How to Use CurrentPrincipal
date: 2015-02-12 05:48
author: weliwita@gmail.com
comments: true
categories: [Authentication, Claims, Identity]
---
The user running a .Net application is identified by the <code>Thread.CurrentPrincipal</code> property of the running thread. You can set the CurrentPrincipal at application startup as follows.
<code></code>
<pre class="lang:c# decode:true ">string[] roles = { "Manager", "Administrator" };
Thread.CurrentPrincipal = new GenericPrincipal(
new GenericIdentity("John"), roles);</pre>
Then later you can make authorization decisions based on the current user.
<pre class="lang:c# decode:true ">if (!System.Threading.Thread.CurrentPrincipal.IsInRole("Manager"))
{
    Console.WriteLine("Permission denied");
    return;
}
else{
    Console.WriteLine("Permission granted");
    return;
}</pre>
<h4>Related Links</h4>
<a title="msdn documentation" href="https://msdn.microsoft.com/en-us/library/system.threading.thread.currentprincipal(v=vs.110).aspx">msdn documentation</a>
