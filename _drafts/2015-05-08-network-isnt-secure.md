---
layout: post
title: Network Isn't Secure
date: 2015-05-08 06:04
author: weliwita@gmail.com
comments: true
categories: [security basics, Security Fundamentals]
---
L. Peter Deutsch, of Sun Microsystems, is credited with penning the first seven fallacies of distributed computing in 1994.  James Gosling the inventor of Java, added the eighth fallacy to the list.

The fallacies of distributed computing are as follows.

<ol>
	<li>The network is reliable.</li>
	<li>Latency is zero.</li>
	<li>Bandwidth is infinite.</li>
	<li><b>The network is secure.</b></li>
	<li>Topology doesn't change.</li>
	<li>There is one administrator.</li>
	<li>Transport cost is zero.</li>
	<li>The network is homogeneous.</li>
</ol>

There are many reasons why network is not secure. The main point is that you should never trust the input from network by default. 

What are the technologies that comes to rescue?
<ul>
	<li>SSL - is used to provide transport layer security</li>
	<li>Message encryption - provides message level security.</li>
</ul>


So you must use any of the above technologies when you deliver confidential messages across network. 
