---
layout: post
title:  "How to use ini file in C++"
date:   2017-09-13 12:43:53 +0900
categories: C/C++
---

Use .ini methods, supported by Windows API to set environment variables for C++ applications.
-To Read
{% highlight cpp %}
GetPrivateProfileString(
  __in   LPCTSTR lpAppName,
  __in   LPCTSTR lpKeyName,
  __in   LPCTSTR lpDefault,
  __out  LPTSTR lpReturnedString,
  __in   DWORD nSize,
  __in   LPCTSTR lpFileName
);
{% endhighlight %}

-To Write
{% highlight cpp %}
WritePrivateProfileString(
  __in  LPCTSTR lpAppName,
  __in  LPCTSTR lpKeyName,
  __in  LPCTSTR lpString,
  __in  LPCTSTR lpFileName
);
{% endhighlight %}

ex)
init.ini
{% highlight cpp %}
-------------------------
[INPUT_VAL]
val1 = Test1
val2 = Test2
--------------------
{% endhighlight %}

To load .ini parameters,

{% highlight cpp %}
char
Temp[100];
GetPrivateProfileString("INPUT_VAL","val1","NOT_FOUND",Temp,100,"./init.ini");
{% endhighlight %}


To Write .ini parameters,

{% highlight cpp %}
WritePrivateProfileString(("INPUT_VAL","val1","Test10","./init.ini");
{% endhighlight %}



