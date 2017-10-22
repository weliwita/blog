---
layout: post
title: "How to use Identity in a .NET Web Application : Part-1"
date: 2015-02-15 08:57
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, Identity and Access Management]
tags: [authentication, claims]
---
In a previous [post](/visual%20studio/identity%20and%20access%20management/2015/02/12/how-to-use-currentprincipal.html), I described how does a user is represented inside a DotNet application using `Thread.CurentPrinciple` property. In this post and next, I will go through the default visual studio 2013 MVC template to see how the identity is set for an MVC application.

Let's say in the default template you put authorize attribute in the `About` action in `Home` controller like follows.

{% highlight csharp %}
[Authorize]
public ActionResult About()
{
    ViewBag.Message = "Your application description page.";
    return View();
}
{% endhighlight %}

If you now try to navigate to `/Home/About` you will receive is a `302` redirect to `/Account/Login?ReturnUrl=%2FHome%2FAbout`

Let's see what is happening inside the OWIN pipeline.

To get details within OWIN pipeline we can inject some additional logging components as follows. Here we have injected two middleware components before and after cookie authentication middleware.

{% highlight csharp %}
app.Use(async (Context, next) =>
{
    Debug.WriteLine("1 ==>request, before cookie auth");
    Debug.WriteLine("1 ==>context.response="+ Context.Response.StatusCode);
    await next.Invoke();
    Debug.WriteLine("4 <==response, after cookie auth");
    Debug.WriteLine("4 ==>context.response=" + Context.Response.StatusCode);
}); 

app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    AuthenticationType = DefaultAuthenticationTypes.ApplicationCookie,
    LoginPath = new PathString("/Account/Login"),
    ...
});

app.Use(async (Context, next) =>
{
    Debug.WriteLine("2 ==>context.response=" + Context.Response.StatusCode);
    Debug.WriteLine("2 ==>request, before controller action");
    await next.Invoke();
    Debug.WriteLine("3 <==response, after controller action");
    Debug.WriteLine("3 ==>context.response=" + Context.Response.StatusCode);
});
{% endhighlight %}

If you now issue a request to `/Home/About` page you get following debug output.

```
1 ==>request, before cookie auth
1 ==>context.response=200
2 ==>context.response=200
2 ==>request, before controller action
3 <==response, after controller action
3 <==context.response=401
4 <==response, after cookie auth
4 <==context.response=302
```

See how response changed from 200 to 401 after the controller action. The `Authorize` attribute has detected that `Thread.CurentPrinciple` doesn't contain a valid identity and has issued a `401 Unauthorized` response.

This `401` response then go through the cookie authentication middleware and it then changes the `401 Unauthorized` into `302 Redirect`. The cookie authentication middleware knows where user should be redirected to get authenticated by using the `LoginPath`
property. It also knows the URL user originally requested. So it can easily construct the redirect URL to the login page as follows

`/Account/Login?ReturnUrl=%2FHome%2FAbout`

Let's see how login process takes place in the next post.

### References
Brock Allen has this great <a href="http://brockallen.com/2013/10/24/a-primer-on-owin-cookie-authentication-middleware-for-the-asp-net-developer/" title="article">article </a>about the cookie authentication middleware.

