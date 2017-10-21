---
layout: post
title: Block, inline and inline-block distilled
date: 2016-08-20 02:36
author: weliwita@gmail.com
comments: true
categories: [CSS, FrontEnd]
---
CSS is always confusing for me.



<a href="https://devhumor.com/media/css">https://devhumor.com/media/css</a>

Here are some basics.

HTML elements can be any of following three basic types.
<ol>
 	<li>Block (e.g. div,p)</li>
 	<li>Inline (e.g. span)</li>
 	<li>Inline-Block (e.g. button, input)</li>
</ol>
To check which element is which you can set the background-color CSS property for that element. Then you can see 'Block'elements stretch the full width and height of the container while 'Inline' elements only stretch its content.

There are few other differences as well
<table>
<colgroup> <col style="width: 33%;" /> <col style="width: 33%;" /> <col style="width: 34%;" /> </colgroup>
<tbody>
<tr>
<th valign="top">Block</th>
<th valign="top">Inline</th>
<th valign="top">Inline-block</th>
</tr>
<tr>
<td valign="top">Stack on top of each other</td>
<td valign="top">Stack horizontally</td>
<td valign="top">Stack horizontally</td>
</tr>
<tr>
<td valign="top">size related CSS can be applied e.g.padding,margin,width,height</td>
<td valign="top">Width and height are of the content.Margin and padding have unexpected behavior</td>
<td valign="top">size related CSS can be applied
padding,margin,width,height</td>
</tr>
</tbody>
</table>
You can always set the element type as a display property of CSS.

HTH!
