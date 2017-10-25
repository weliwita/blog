---
layout: post
title: HTML Helper to Display the Logged In User's DisplayName
date: 2015-03-22 07:01
author: weliwita@gmail.com
comments: true
categories: [Visual Studio, IAM]
tags: [claims]
---
It is pretty common to display the logged-in user in various places in a website. We can create an HTML helper to display the logged-in user's name.

{% highlight csharp %}
        public static MvcHtmlString UserDisplayName(this HtmlHelper htmlHelper)
        {
            if (htmlHelper.ViewContext.HttpContext.Request.IsAuthenticated)
            {
                ClaimsPrincipal principal = htmlHelper.ViewContext.HttpContext.User as ClaimsPrincipal;
                if (principal == null)
                {
                    throw new InvalidCastException("The current principal is not a claims principal.");
                }

                var nameClaim = principal.Claims.FirstOrDefault(t => t.Type == "name"); //use any claim that need to be displayed as UserDisplayName
                if (nameClaim != null)
                {
                    return new MvcHtmlString(nameClaim.Value);
                }
            }

            return new MvcHtmlString("Anonymous");

        }
{% endhighlight %}

Then the helper can be used on the navigation bar or any other UI widget that need to display user name.

{% highlight html %}
             <ul class="nav navbar-nav navbar-right">  
                    <li class="dropdown navbar-text">
                        Hi, @Html.UserDisplayName()
                    </li>
             </ul>
{% endhighlight %}


