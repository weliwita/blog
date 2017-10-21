---
layout: post
title: What's behind the login screen?  How modern applications know who you are and what you allow it to do.
date: 2015-05-05 06:01
author: weliwita@gmail.com
comments: true
categories: [Authentication, Identity, Identity, OAuth2, security basics]
---
<h3>The Problem</h3>
With the rise of the cloud services, protecting the personal bits and bytes becomes very important. Large companies like Google, Apple, Facebook, Microsoft and Twitter has a lot of information about their users. But sharing that information with other 3rd party applications was a big issue in the past. For example, if you share your google password with a 3rd party application you are trying to access, that application can impersonate you with the shared password, access your email, read your calendar, access your google drive etc.

On the other hand if you don't share your personal data among applications you have to enter your personal information(first name, last name, email, etc..) to each application you visit and remember the password for each application.(you know how hard it is to manage all username password combinations you already have)
<h3>The solution</h3>
I think you have seen the solution in action when you try to sign up to an application hosted on the cloud. Let's discuss each step at the high level using an example. This example is used only to illustrate the general concepts, the actual underlying implementation might differ from the content of this article.
<h4>Selecting the Identity Provider(IP)</h4>
First, you must select an identity provider. Identity Provider(or IP in short) play a major role in modern authentication and authorization scenarios.
When you click sign up (to stackoverflow application in this example) you will present a screen similar to following to select an IP.
<a href="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2016/03/Chose-The-Identity-Provider.png" rel="attachment wp-att-230"><img src="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2016/03/Chose-The-Identity-Provider-300x220.png" alt="Chose-The-Identity-Provider" width="300" height="220" class="alignnone size-medium wp-image-230" /></a>

An IP is some authority that knows about both the user and the application. Among other things, it can provide information about the user to the application via tokens. The main problem is that different IPs implement different protocols and the application should communicate with each IP differently(i.e you can't use the code written to use Google as IP and talk to Facebook or vice-versa). What it means is that it was very hard to add new IP to an application without adding new code. I will discuss this specific problem and the solution(OpenId Connect) in a future post.

After you have selected an IP, Google in this case, redirection happens to the selected IP's authentication endpoint.
<code>
https://accounts.google.com/ServiceLogin?service=lso&amp;passive=1209600&amp;continue=https://accounts.google.com/o/oauth2/auth?response_type%3Dcode%26scope%3Dprofile%2Bemail%26redirect_uri%3Dhttps://stackauth.com/auth/oauth2/google%26state%3D%257B%2522sid%2522:1,%2522st%2522:%2522fc45ef47f10680ee229ab6cbdb341bd3afa6980a3cf0f7d249f9e936e0075c2e%2522,%2522ses%2522:%2522fd7412355e94469182466192a6bee2f1%2522%257D%26client_id%3D717762328687-p17pldm5fteklla3nplbss3ai9slta0a.apps.googleusercontent.com%26hl%3Den-US%26from_login%3D1%26as%3D75bea02b9a35523&amp;ltmpl=popup&amp;shdf=CrYCCxIRgM1wx9Gk3pYa4vlfcQQcQs2oA&amp;sarp=1&amp;scc=1
</code>
The protocol used here is OAuth2. It is an authorization protocol rather than authentication protocol. So different companies used different authentication layers on top of oAuth2. Lets discuss about OAuth2 in a future post.
<h4>Log In to the Identity Provider</h4>
At this point if you are not already logged in to the IP, you are presented with a log-in screen. As you can see, log-in happen in the IP's domain, Application know nothing about your credentials.
<a href="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2016/03/LoginPage.png" rel="attachment wp-att-233"><img src="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2016/03/LoginPage-203x300.png" alt="LoginPage" width="203" height="300" class="alignnone size-medium wp-image-233" /></a>

After a successful log-in IP knows who you are. IP also know which application redirected you to the IP for authentication by inspecting the Client_id in query string. IP then check the scope parameter included in the query string against scopes defined at application registration to determine if this application is allowed to access requested scopes.
<h5>Scopes</h5>
Scopes are a way to partition the protected resources. Protected resources can be your personal information like firstname, lastname, birthday, contacts, calandar, locatioin, etc.
<h4>Consent Screen</h4>
The application is usually only allowed to <em>request the access</em> to a resource. The user can <em>deny</em> application accessing some resources in consent screen.
<a href="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2016/03/TheConsentScreen.png" rel="attachment wp-att-236"><img src="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2016/03/TheConsentScreen-300x273.png" alt="TheConsentScreen" width="300" height="273" class="alignnone size-medium wp-image-236" /></a>

After the consent is given, the application receives a <em>code</em> which can be traded for an access-token.
<h4>Access-token and code</h4>
<code>
https://stackoverflow.com/users/oauth/google?code=4/JrElQmD62a4z52ScIo6twAqqmLuLtBlfhQlLg04.okT1Ke0r3cUTcp7tdiljKKZddTsamgI&amp;state=%7b%22sid%22%3a1%2c%22st%22%3a%22fc45ef47f10680ee229ab6cbdb341bd3afa6980a3cf0f7d249f9e936e0075c2e%22%2c%22ses%22%3a%22fd7412355e94469182466192a6bee2f1%22%7d&amp;s=fd7412355e94469182466192a6bee2f1#
</code>
The application uses access token to get access to a protected resource without knowing your credentials. The resources application can access is limited by scopes. So it can't access all the resources you have access to. Therefore, you are protected from giving unnecessary permissions to the application.
<h3>The Technologies</h3>
There are several technologies attempted to solve the cloud identity problem.
In the early days, WS-* Protocols and SAML tokens were dominating this area. But the popularity of mobile devices forces the industry towards more lightweight protocols. OAuth and OpenIdConnect are the prominent protocols nowadays.

Let's discuss more how the protocols work together to provide the solution in next post.
