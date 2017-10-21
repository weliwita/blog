---
layout: post
title: CSS Positioning
date: 2016-11-23 06:16
author: weliwita@gmail.com
comments: true
categories: [FrontEnd]
---
CSS Positioning can be done in several ways.


<table id="css-positioning-table"><colgroup> <col style="width: 20%;" /> <col style="width: 25%;" /> <col style="width: 55%;" /> </colgroup>
<tbody>
<tr>
<th valign="top">Type</th>
<th valign="top">Style</th>
<th valign="top">Comments</th>
</tr>
<tr>
<td valign="top">fixed</td>
<td valign="top">position:fixed;</td>
<td valign="top">Element is fixed to browser window. Other elements ignore its width and height</td>
</tr>
<tr>
<td valign="top">absolute</td>
<td valign="top">position:absolute;</td>
<td valign="top">Element is fixed to the container. Other elements ignore its width and height</td>
</tr>
<tr>
<td valign="top"> relative</td>
<td valign="top"> position: relative</td>
<td valign="top"> Other elements position retained. top, bottom, etc... move the element relative to the default position.</td>
</tr>
<tr>
<td valign="top"> static</td>
<td valign="top"> position: static</td>
<td valign="top">Default behavior. top, bottom, etc.. properties don't apply.</td>
</tr>
<tr>
<td valign="top"> inherit</td>
<td valign="top"> position: inherit</td>
<td valign="top">Inherit position property from the parent container.</td>
</tr>
</tbody>
</table>
