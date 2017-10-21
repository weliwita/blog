---
layout: post
title: Running web application locally as a predefined user using OWIN Middleware
date: 2015-03-01 09:29
author: weliwita@gmail.com
comments: true
categories: [Authentication, Claims, Identity, Middleware, OWIN, OWIN]
---
It is quite common that we sometimes need to run the application without all the identity server redirection dance at development time. It is posible to assign common identity to all the users running the application locally as follows.

Create a custom authentication middleware as follows.

<pre>

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
</pre>


Then use the custom authentication middleware in the application startup

<pre>
app.Use(typeof(LocalAuthenticationMiddleware));
</pre>


Access the claims via <code>Controller.User</code> API.
<pre>
var nameClaim = (User as ClaimsPrincipal).Claims.FirstOrDefault(t => t.Type == "name");
</pre>

<h4>Related Links</h4>
<a href="https://lbadri.wordpress.com/2013/07/13/basic-authentication-with-asp-net-web-api-using-owin-middleware/">basic authentication</a>

Thanks!

