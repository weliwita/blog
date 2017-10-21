---
layout: post
title: STRIDE Threat & Mitigation Techniques List
date: 2015-06-30 11:58
author: weliwita@gmail.com
comments: true
categories: [security basics, Security Fundamentals]
---
STRIDE is the acronym for six most famous threat categories.

Following list show those categories and known ways to mitigate threats.

This is a extract from owasp article <a href="https://www.owasp.org/index.php/Application_Threat_Modeling">here</a>.

&nbsp;

&nbsp;
<table cellspacing="1" cellpadding="7">
<tbody>
<tr bgcolor="#cccccc">
<th>Threat Category</th>
<th>Mitigation Techniques</th>
</tr>
<tr bgcolor="#cccccc">
<td>Spoofing Identity</td>
<td>
<ol>
	<li>Appropriate authentication</li>
	<li>Protect secret data</li>
	<li>Don't store secrets</li>
</ol>
</td>
</tr>
<tr bgcolor="#cccccc">
<td>Tampering with data</td>
<td>
<ol>
	<li>Appropriate authorization</li>
	<li>Hashes</li>
	<li>MACs</li>
	<li>Digital signatures</li>
	<li>Tamper resistant protocols</li>
</ol>
</td>
</tr>
<tr bgcolor="#cccccc">
<td>Repudiation</td>
<td>
<ol>
	<li>Digital signatures</li>
	<li>Timestamps</li>
	<li>Audit trails</li>
</ol>
</td>
</tr>
<tr bgcolor="#cccccc">
<td>Information Disclosure</td>
<td>
<ol>
	<li>Authorization</li>
	<li>Privacy-enhanced protocols</li>
	<li>Encryption</li>
	<li>Protect secrets</li>
	<li>Don't store secrets</li>
</ol>
</td>
</tr>
<tr bgcolor="#cccccc">
<td>Denial of Service</td>
<td>
<ol>
	<li>Appropriate authentication</li>
	<li>Appropriate authorization</li>
	<li>Filtering</li>
	<li>Throttling</li>
	<li>Quality of service</li>
</ol>
</td>
</tr>
<tr bgcolor="#cccccc">
<td>Elevation of privilege</td>
<td>
<ol>
	<li>Run with least privilege</li>
</ol>
</td>
</tr>
</tbody>
</table>
