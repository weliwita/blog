---
layout: post
title: VS Code Integrated Terminal with Visual Studio Command Prompt
date: 2017-01-21 00:43
author: weliwita@gmail.com
comments: true
categories: [Visual Studio]
tags: [vscode]

---
It is quite convenient to use visual studio developer command prompt from VS Code integrated terminal.

1. You need to find the correct command line argument to start the visual studio command prompt. You can do that by checking properties of the shortcut icon.
![Configuring shortcut]({{ "/assets/img/posts/20170121-Shortcut.png" | absolute_url }})


2. Copy the shortcut link text

{% highlight bat %}
%comspec% /k ""C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\Tools\VsDevCmd.bat""
{% endhighlight %}

3. Then go to user preferences of VS Code and update the ShellArgs property with correct parameters you copied from the step 2.

{% highlight json %}
"terminal.integrated.shellArgs.windows": ["/k", "C:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\Tools\\VsDevCmd.bat"]
{% endhighlight %}

4. If everything goes ok you should be able to use developer command prompt within VS Code integrated shell as follows
![Using command prompt]({{ "/assets/img/posts/20170121-Compiling.png" | absolute_url }})

------------

### Troubleshooting

If you have trouble executing commands you can check if correct command parameters are passed into the integrated terminal by using the process explorer.
[![Using process explorer]({{ "/assets/img/posts/20170121-CommandLine.png" | absolute_url }})]({{ "/assets/img/posts/20170121-CommandLine.png" | absolute_url }})


If you are running an older version of VS Code you may need to upgrade to the latest version due to this [bug](https://github.com/Microsoft/vscode/issues/7266) 
