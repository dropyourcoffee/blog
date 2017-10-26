---
layout: post
title:  "Use of extern C"
date:   2017-07-05 12:43:53 +0900
categories: Embedded/C_C++
---

In C++17, new `__cpluscplus` was defined as 201703L.

{% highlight c %}
#ifdef __cplusplus
extern "C" {
#endif

...

#ifdef __cplusplus
}
#endif

{% endhighlight %}

We use the macro as above to compile the C code with g++ compiler.

In C++, in order to support features such as function overloading, C functions are given different names, hence without `extern "C"` the module won't be discovered by the linker.
(`extern C` lets the C module avoid the [name mangling](http://www.geeksforgeeks.org/extern-c-in-c/)).
