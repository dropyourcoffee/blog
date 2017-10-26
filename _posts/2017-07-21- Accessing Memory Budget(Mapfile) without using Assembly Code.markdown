---
layout: post
title:  "Accessing memory budget in C (instead of assembly)"
date:   2017-07-21 12:43:53 +0900
categories: Embedded/C_C++
---

#### 1. Label the memory symbols in assembly file(startup_<device>.s).


{% highlight assembly %}
Load__SRAM__Base
    DCD |Load$$SRAM$$Base|

Image__SRAM__Base
    DCD |IMAGE$$SRAM$$Base|

Image__SRAM__Length
    DCD |Image$$SRAM$$Length|

Image __SRAM__ZI_Base
    DCD |Image$$SRAM$$ZI$$Base|

Image __SRAM__ZI__Length
    DCD |Image$$SRAM$$ZI$$Length|

...

{% endhighlight %}

#### 2. Declare the symbols as extern in C.

{% highlight c %}
extern byte *Image__SRAM__Base;
extern byte *Image__SRAM__Length;
extern byte *Load__SRAM__Base;
extern byte *Image__SRAM__ZI__Base;
extern byte *Image__SRAM__ZI__Length;

{% endhighlight %}

Use casting to reference different size.

#### 3. How to initialize RW regions(global variables with non-zero initial values)

{% highlight c %}
end_point = (dword *)((dword)Image__SRAM__Base + (dword)Image__SRAM__Length);

for(src = (dword*) Load__SRAM__Base,
    dst = (dword*) Image__SRAM__Base;  dst<end_point; src++,dst++)
{
  *dst = *src;
}


{% endhighlight %}