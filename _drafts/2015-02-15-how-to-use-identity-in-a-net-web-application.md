---
layout: post
title: How to use Identity in a .NET Web Application
date: 2015-02-15 08:57
author: weliwita@gmail.com
comments: true
categories: [Authentication, Claims, Identity]
---
If you have a look at asp.net MVC5 default template's 'ConfigureAuth' code, you will see following code.
<pre class="">  
app.UseCookieAuthentication(new CookieAuthenticationOptions
            {
                AuthenticationType = DefaultAuthenticationTypes.ApplicationCookie,
                LoginPath = new PathString("/Account/Login"),
                Provider = new CookieAuthenticationProvider
                {
                    // Enables the application to validate the security stamp when the user logs in.
                    // This is a security feature which is used when you change a password or add an external login to your account.  
                    OnValidateIdentity = SecurityStampValidator.OnValidateIdentity&lt;ApplicationUserManager, ApplicationUser&gt;(
                        validateInterval: TimeSpan.FromMinutes(30),
                        regenerateIdentity: (manager, user) =&gt; user.GenerateUserIdentityAsync(manager))
                }
            });       
</pre>

The main idea is that CookieAuthentication middleware sits in the OWIN pipeline. It sets the user's identity to a ClaimsPrincipal by reading and validating the cookie it issued when the user is logged in. 

We can then use following APIs to get the Identity information about the user.

<pre>
Page.User,
Controller.User,
HttpContext.User,
Thread.CurrentPrincipal,
ClaimsPrincipal.Current
</pre>

<h4>Related Links</h4>
Brock Allen has this great <a href="http://brockallen.com/2013/10/24/a-primer-on-owin-cookie-authentication-middleware-for-the-asp-net-developer/" title="article">article </a>about the cookie authentication middleware.

