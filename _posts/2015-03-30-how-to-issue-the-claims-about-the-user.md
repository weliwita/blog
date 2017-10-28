---
layout: post
title: How to Issue the Claims About the User
date: 2015-03-30 11:43
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, IAM]
tags: [authentication, claims]
---

This post is part of few introductory blog posts about the identity in DotNet Application. In this post, let's talk about the process of storing and issuing claims about the user.

The claims are basically key-value pairs that say something about the authenticated user. These key-value pairs should be stored somewhere against the user's identity. As we are going through the default ASP.NET template, Let's see how claims are stored in the DB.

You can see following connection string in the web.config file

{% highlight xml %}
<add name="DefaultConnection" connectionString="Data Source=(LocalDb)\v11.0;AttachDbFilename=|DataDirectory|\aspnet-AuthenticationExamples-20171022124844.mdf;Initial Catalog=aspnet-AuthenticationExamples-20171022124844;Integrated Security=True"
      providerName="System.Data.SqlClient" />
{% endhighlight %}

Let's use either server explorer or SQL server management studio to see the DB.

[![IdentityDB]({{ site.baseurl }}/assets/img/posts/20170330-IdentityDB.png)]({{ site.baseurl }}/assets/img/posts/20170330-IdentityDB.png)

As you can see `ASPNETUserClaims` table store the `ClaimType` and `ClaimValue` pairs against `UserId`.

Now let's see how we these values are stored and retrieved using code.

Let's create simple console app and use the default connection string(see above) used in asp.net default template.

```
PM> Install-package Microsoft.AspNet.Identity.Core -Version 2.2.1
PM> Install-package Microsoft.AspNet.Identity.EntityFramework -Version 2.2.1
```

The SignInManager uses the UserManager class internally to validate user password. UserManager is the main service that store and retrieve users and claims from the data store.

So using our console app we can add a claim for an existing user as follows

{% highlight csharp %}
var userStore = new UserStore<IdentityUser>();
var userManager = new UserManager<IdentityUser, string>(userStore);
var user = userManager.FindByEmail("weliwita@gmail.com");
var claim = new IdentityUserClaim();
claim.ClaimType = ClaimTypes.Role;
claim.ClaimValue = "Administrator";
user.Claims.Add(claim);
userManager.Update(user);
{% endhighlight %}

[![IdentityDB]({{ site.baseurl }}/assets/img/posts/20170330-ClaimsInCode.png)]({{ site.baseurl }}/assets/img/posts/20170330-ClaimsInCode.png)


Similarly, we can retrieve claims from user manager as follows

{% highlight csharp %}
var userStore = new UserStore<IdentityUser>();
var userManager = new UserManager<IdentityUser, string>(userStore);
var user = userManager.FindByEmail("weliwita@gmail.com");
var claims = user.Claims;
{% endhighlight %}


[![IdentityDB]({{ site.baseurl }}/assets/img/posts/20170330-ClaimsListInCode.png)]({{ site.baseurl }}/assets/img/posts/20170330-ClaimsListInCode.png)

UserManager is capable of performing many tasks related user. e.g account lockout, two-factor authentication using SMS service etc... See the [documentation](https://msdn.microsoft.com/en-us/library/dn613290(v=vs.108).aspx) for more details. 

Now we know how claims are stored and retrieved using the ASP.NET default template. The template uses libraries(see Nuget Packages above) belong to ASP.NET Identity. There are other similar libraries to manage users and claims. Membership reboot is one such library(Update-It is deprecated as of 2017).

In the default template, UserManagement is part of the application itself. As you can see in the template itself, it is a lot of code and learning curve for an application developer. So nowadays applications tend not to handle user management.

If an application doesn't want to handle user management who can? Let's discuss it in another post.

