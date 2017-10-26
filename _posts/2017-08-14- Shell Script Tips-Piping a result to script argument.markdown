---
layout: post
title:  "Shell script Tip - Piping a result to script argument"
date:   2017-08-14 12:43:53 +0900
categories: Linux/Bash
---

While writing a script for a jobs scheduling or for any kind of deployment, it is sometimes needed to 
pass the output of a command to an argument of the script.

In such case,

{% highlight sh %}
$ touch script.rc
$ chmod u+x script.rc
$ vim script.rc
{% endhighlight %}

{% highlight shell %}
#!bin/bash

echo "Hello $(cat)"
{% endhighlight %}
