---
layout: post
title: "ctfshow,贝斯多少呢"
categories: crypto
tags: base62
excerpt: ctfshow做题的wp，本文章关于base编码。
data: 2021-08-09
author: citytwilight
---

# 题目

https://ctf.show/challenges#%E8%B4%9D%E6%96%AF%E5%A4%9A%E5%B0%91%E5%91%A2-252



# 解题过程

#### step1：分析

分析题目给的的什么编码方式，感觉有点像base，至于是base多少不知道

```
8nCDq36gzGn8hf4M2HJUsn4aYcYRBSJwj4aE0hbgpzHb4aHcH1zzC9C3IL
```

#### step2：解密

利用[bugku工具](https://ctf.bugku.com/tools)尝试了各种base，发现只有base62能够解出

```
12896984793086997065170080376052401406200954459728780801006439132646467311747317647095566113334919954432
```

但是这一串加密后与原来的不同，放弃。

然后别人提示是国外base62，最后找到了网站http://decode-base62.nichabi.com/

![](D:\桌面\刷题\markdown\图片\12.png)

#### step3：得到flag

```
flag{6a5eb2_i5_u5ua11y_u5ed_f0r_5h0rt_ur1}
```



# 思考总结

对于一些常见的编码方式还能识别出来，这种比较冷门的不知道，而且国外base62编码貌似和bugku的有区别。



解决：积累，了解常见的编码方式，做到能够识别出来。
