---
layout: post
title: Running web application locally as a predefined user using OWIN Middleware
date: 2015-03-01 09:29
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, IAM]
tags: [authentication, claims]
---

It is quite common that we sometimes need to run the application without all the identity server redirection dance at development time. It is possible to assign common identity to all the users running the application locally as follows.

Create a custom authentication middleware as follows.

{% highlight csharp %}
public class LocalAuthenticationMiddleware : OwinMiddleware
{
    
    public LocalAuthenticationMiddleware2(OwinMiddleware next) :
        base(next) { }

    public override async Task Invoke(IOwinContext context)
    {
        var response = context.Response;
        var request = context.Request;

        response.OnSendingHeaders(state =>
        {
            var resp = (OwinResponse)state;

            if (resp.StatusCode == 401)
            {
                resp.Headers.Add("WWW-Authenticate", new[] { "Basic" });
                resp.StatusCode = 403;
                resp.ReasonPhrase = "Forbidden";
            }
        }, response);

        // use this identity only if running locally
        if (request.Uri.IsLoopback)
        {
            var claims = new[]
                    {
                        new Claim("name", "Administrator"),
                        new Claim(ClaimTypes.NameIdentifier, "0001"),
                        new Claim(ClaimTypes.Role, "SiteAdministrator"),
                    };
            var identity = new ClaimsIdentity(claims, "Basic");
            request.User = new ClaimsPrincipal(identity);

        }

        await Next.Invoke(context);
    }
}
{% endhighlight %}


Then use the custom authentication middleware in the application startup

{% highlight csharp %}
app.Use(typeof(LocalAuthenticationMiddleware));
{% endhighlight %}


Access the claims via `Controller.User` API.
{% highlight csharp %}
var nameClaim = (User as ClaimsPrincipal).Claims.FirstOrDefault(t => t.Type == "name");
{% endhighlight %}

### References
<a href="https://lbadri.wordpress.com/2013/07/13/basic-authentication-with-asp-net-web-api-using-owin-middleware/">basic authentication</a>

