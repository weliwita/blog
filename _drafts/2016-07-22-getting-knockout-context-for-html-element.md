---
layout: post
title: Getting knockout context for html element.
date: 2016-07-22 06:59
author: weliwita@gmail.com
comments: true
categories: [Uncategorized]
---
This small code helps me a lot to get the knockout context for a given element.
<pre class="lang:default decode:true ">var x = ko.contextFor(document.getElementById('Agreement_AgreementCode')) 
x.$data.Agreement.AgreementCode()</pre>
&nbsp;
