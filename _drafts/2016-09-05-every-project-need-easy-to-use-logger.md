---
layout: post
title: Every project need easy to use logger
date: 2016-09-05 05:49
author: weliwita@gmail.com
comments: true
categories: [Uncategorized]
---
I found the following pattern for getting and configuring loggers very useful.

In your startup, you configure your logger.
<pre class="lang:default decode:true "> LogProvider.SetCurrentLogProvider(new TraceSourceLogProvider());</pre>
In your service or controller, you get logger instance
<pre class="lang:default decode:true ">private readonly static ILog Logger = LogProvider.GetCurrentClassLogger();</pre>
&nbsp;

&nbsp;
