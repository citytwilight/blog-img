---
layout: post
title: "ctfshow,萌新_密码5"
categories: crypto python
tags: 当铺密码 
excerpt: ctfshow做题的wp，本文章关于当铺密码。
data: 2021-07-30
author: citytwilight
---

# 题目

https://ctf.show/challenges#%E8%90%8C%E6%96%B0_%E5%AF%86%E7%A0%815-110



# 解题过程

#### step1：分析

看着题目给的东西懵了，后来经过百度以及看wp得知是当铺密码

```
由田中 由田井 羊夫 由田人 由中人 羊羊 由由王 由田中 由由大 由田工 由由由 由由羊 由中大
```

#### step2：脚本解密

```
s ='田由中人工大王夫井羊'
code=input("请输入当铺密码：")
code = code.split(" ")
w = ''
for i in code:
    k=""
    for j in i:
       k+=str(s.index(j))
    w+=chr(int(k))
print(w)

```



#### step3：得到flag

```
请输入当铺密码：由田中 由田井 羊夫 由田人 由中人 羊羊 由由王 由田中 由由大 由田工 由由由 由由羊 由中大
flag{ctfshow}
```



# 思考总结

奇奇怪怪的，没见过的密码太多了

解决：多积累吧

