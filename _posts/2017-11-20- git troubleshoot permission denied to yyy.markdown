---
layout: post
title:  "Troubleshoot :: Permission to xxx/repos.git denied to yyy"
date:   2017-11-20 11:43:53 +0900
tags: Troubleshoot git
categories: Linux/bash
---



remote: Permission to xxx/repos.git denied to yyy.

happens when I initially made a git repository with credential xxx and try to push a branch with credential yyy.

Setting up user

`git config github.user xxx` did not work

instead, I solved by adding my local machine's ssh key to my github account and worked.

Make public key.
{% highlight sh %}
ssh-keygen
{% endhighlight %}

Go to your github page, click (your account icon on top-right) - Settings - SSH And GPG Keys.
Copy your generated key (~/.ssh/id_rsa.pub) and paste it with a title.

Retry git push again through ssh.
Assuming your remote respository named, origin:
{% highlight sh %}
git remote rm origin
git remote add origin github@github.com:<gitAccount>/<respos name>.git
git remote -v # check remote repository
git push origin <branch name>
{% endhighlight %}



