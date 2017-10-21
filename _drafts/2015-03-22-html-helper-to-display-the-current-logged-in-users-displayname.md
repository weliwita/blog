---
layout: post
title: HTML Helper to Display the Current Logged In User's DisplayName
date: 2015-03-22 07:01
author: weliwita@gmail.com
comments: true
categories: [Claims, Identity, Identity, MVC]
---
It is pretty common to display the current logged-in user in various places in a website. We can create an HTML helper to display the current logged-in user's name.

<pre>
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
</pre>

Then the helper can be used on the navigation bar or any other UI widget that need to display user name.

<pre>
             <ul class="nav navbar-nav navbar-right">  
                    <li class="dropdown navbar-text">
                        Hi, @Html.UserDisplayName()
                    </li>
             </ul>
</pre>

<a href="http://www.weliwita.com/blog/wp-content/uploads/2015/03/TopBar.png"><img src="http://www.weliwita.com/blog/wp-content/uploads/2015/03/TopBar.png" alt="TopBar" width="1168" height="53" class="alignnone size-full wp-image-62" /></a>

Thanks!

