---
layout: post
title:  "Troubleshoot :: ranlib"
date:   2017-09-15 12:43:53 +0900
tags: ranlib
categories: Linux/bash
---

While installing a package through Makefile I got an error code :

`ranlib: /usr/lib64/libelf.so.1:version 'ELFUTILS_1.1.1' not found(required by ranlib)`

After a few google search, I replaced the `ranlib` with `ar -s` in the script and installation completed successfully.

{% highlight sh %}
$ man ranlib
Generates an index to the contents of an archive and stores it in the archive.

$ man ar
Create, modify, and extract from archives
-s   Add an index to the archive, or update it if it already exists.  Note this command is an exception to the rule that there can only be one command letter, as it is
possible to use it as either a command or a modifier.  In either case it does the same thing.
{% endhighlight sh %}

