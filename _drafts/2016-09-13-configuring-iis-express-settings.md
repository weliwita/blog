---
layout: post
title: Configuring IIS Express Settings
date: 2016-09-13 12:04
author: weliwita@gmail.com
comments: true
categories: [Configuration]
---
I'm sometimes getting very frustrated debugging sample websites copied from a different directory of my machine. The main problem was even I was debugging the site that was copied, IISExpres actually points to the original folder of that site. So whatever changes I did was not picked up by the IIS express.

To solve the issue you need to edit the IISExpress config file located here.
<pre class="lang:default decode:true">%systemdrive%\Users\&lt;Username&gt;\Documents\IISExpress\config</pre>
Open the ApplicationHost.config file and in the &lt;sites&gt; section, search for your site's name. You will see an element like this:
<pre class="lang:default decode:true ">&lt;site name="WebSite1" id="1" serverAutoStart="true"&gt;
   &lt;application path="/"&gt;
      &lt;virtualDirectory path="/" physicalPath="%IIS_SITES_HOME%\WebSite1" /&gt;
   &lt;/application&gt;
   &lt;bindings&gt;
       &lt;binding protocol="http" bindingInformation=":8080:localhost" /&gt;
   &lt;/bindings&gt;
&lt;/site&gt;</pre>
Change the parameters to anything you want.

E.g.
<pre class="lang:default decode:true">physicalPath="D:\Projects\NetClean\tools\Samples\PhyrenPortal\PhyrenPoral"</pre>
<pre class="lang:default decode:true ">&lt;binding protocol="http" bindingInformation="*:44444:localhost" /&gt;</pre>
You can even bind to a different hostname
<pre class="lang:default decode:true">&lt;binding protocol="http" bindingInformation="*:80:mysite.local" /&gt;</pre>
and then map mysite.local to 127.0.0.1 in your hosts file, and then open your website from "http://mysite.dev";

If you change the <strong>startup port</strong> you need to change your Web Application project as well.
<ol>
 	<li>In Solution Explorer, right-click the name of the project and then select Properties. Click the Web tab.</li>
 	<li>In the Servers section, under Use Local IIS Web server, in the Project URL box enter a URL to match the hostname and port you entered in the ApplicationHost.config file from before.</li>
 	<li>To the right of the Project URL box, click Create Virtual Directory, and then click OK.</li>
 	<li>In the File menu, click Save Selected Items.</li>
</ol>
Now you should be able to browse to your site without any issue.

reference: http://stackoverflow.com/questions/21202885/how-can-i-change-iis-express-port-for-a-site
