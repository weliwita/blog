---
layout: post
title: "How to use Identity in a .NET Web Application - Part 2"
date: 2015-02-15 08:57
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, Identity and Access Management]
tags: [authentication, claims]
---

In the previous blog [post], I described how a `302 Redirect` is issued to the browser when the user requests a page that requires a logged in user. In this post, let's see how the actual login process works in default MVC template.

So, when the browser gets redirect to the  `/Account/Login?ReturnUrl=%2FHome%2FAbout` page, that request is handled by the `Account` controller's `Login` action. It basically returns a form for the user to enter the log-in credentials. Please note that return URL is also sent along.

When the form is submitted back it is submitted to the following action method.

{% highlight csharp %}
public async Task<ActionResult> Login(LoginViewModel model, string returnUrl)
{
    if (!ModelState.IsValid)
    {
        return View(model);
    }
    var result = await SignInManager.PasswordSignInAsync(model.Email, model.Password, model.RememberMe, shouldLockout: false);
    switch (result)
    {
        case SignInStatus.Success:
            return RedirectToLocal(returnUrl);
        case SignInStatus.LockedOut:
            return View("Lockout");
        case SignInStatus.RequiresVerification:
            return RedirectToAction("SendCode", new { ReturnUrl = returnUrl, RememberMe = model.RememberMe });
        case SignInStatus.Failure:
        default:
            ModelState.AddModelError("", "Invalid login attempt.");
            return View(model);
    }
}
{% endhighlight %}

`SignInManager.PasswordSignInAsync()` method is the most important here. It creates the set of claims to represent the identity of the user and creates a `ClaimsIdentity`. It also updates some properties in OWIN pipeline with the identity created so subsequent pipeline stages would know if the user has been authenticated. On the response, the user cookie middleware intercepts and issue a sign-in cookie.

This cookie is then resubmitted on each request to the site. The Cookie authentication middleware can then intercept the request and construct the user identity and set claims principle on the thread processing the request.

We can then use the following APIs to get the Identity information about the user.

```
Page.User,
Controller.User,
HttpContext.User,
Thread.CurrentPrincipal,
ClaimsPrincipal.Current
```

### References
Brock Allen has this great <a href="http://brockallen.com/2013/10/24/a-primer-on-owin-cookie-authentication-middleware-for-the-asp-net-developer/" title="article">article </a>about the cookie authentication middleware.