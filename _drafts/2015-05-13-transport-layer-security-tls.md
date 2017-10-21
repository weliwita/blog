---
layout: post
title: Transport Layer Security (TLS)
date: 2015-05-13 05:42
author: weliwita@gmail.com
comments: true
categories: [security basics, Security Fundamentals]
---
<h4>What is Transport Layer</h4>
In the Open Systems Interconnection(OSI) model the transport layer is most often referred to as Layer 4. It resides between network layer and session layer.
<h3>What is Transport Layer Security (TLS)</h3>
TLS is a protocol designed to provide communications security over a computer network. It is the successor of the SSL. The protocol is defined <a href="http://tools.ietf.org/html/rfc5246">here</a>.
It can provide privacy and data integrity between two communicating applications.
<h4>Why it is important</h4>
It allows unprotected protocols like HTTP to travel across a secure tunnel and adds following features to the HTTP
<ol>

<li>
<h5>Server Authentication</h5>
Make sure that we are talking to the server that we are expecting to call. Without TLS we have no guarantee that the server at the other end of the channel is the same server that we intended to call.This is achieved by using x.509 certificates
</li>
<li>
<h5>Integrity Protection</h5>
Make sure that middleman between client and server can't modify the content. This is also achieved by using x.509 certificates with hashed content.
</li>
<li>
<h5>Replay protection</h5>
Make sure same request can't be repeatedly send to the server.</li>
<li>
<h5>confidentiality</h5>
Make sure the messages client send to the server are properly encrypted so that nobody in the middle cannot see the content on the wire.
</li>
</ol>
In modern web applications TLS is a must ensuring Confidentiality and Integrity without affecting Availability.
