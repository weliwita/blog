---
layout: post
title: Attaching Windbg to Managed Application
date: 2017-04-10 16:47
author: weliwita@gmail.com
comments: true
categories: [Debuging, Windbg]
---
You may want time to time dig into the implementation detail of the code you are working with(e.g. how they are represented in RAM). Windbg with the help of SOS extension gives you lot of those implementation detail. But when the initial breakpoint is hit the CLR has not yet been loaded and Windbg doesn't allow you to load SOS. What you can do here is that temporary set a <code>Console.ReadLine()</code> in your code and hit Ctrl + Break to break the debugger at your desired location.

<script src="https://gist.github.com/weliwita/5b57ce9859b8fd140c09002f991ce395.js"></script>

Launch the executable from WinDbg, and then input "g" command to let debuggee process to continue until readLine statement. press <code>Ctrl + Break</code> or use <code>menu-&gt;Debug-&gt;Break</code> and then input command <code>.loadby sos clr</code> to load the SOS extension.
<h4>The Infinite Loop Technique</h4>
In case you are not working with a console app and you still need to break into a specific location you can use infinite loop technique. In this technique, you are injecting temporary infinite loop, based on the value of a global Boolean flag, into your code.

<script src="https://gist.github.com/weliwita/e40e988b4dd2a53ee6e5cea35622de00.js"></script>

When you hit <code>g</code> in the debugger it will stop at the infinite loop. You can then break into the loop and set the boolean flag to true in memory window. To track the location of the local variable in the stack you can use <code> !clrstack -a </code> command. After setting the variable to true you can continue the execution by hitting <code>g</code> command to get out of the infinite loop.

<a href="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2017/04/Images.png"><img class="alignnone  wp-image-381" src="https://blog-curlybraces.rhcloud.com/wp-content/uploads/2017/04/Images-300x64.png" alt="" width="619" height="132" /></a>
