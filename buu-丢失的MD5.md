---
layout: post
title: "buu,丢失的MD5"
categories: crypto python
tags: MD5 buu
excerpt: buu做题的wp，本文章关于MD5爆破。
data: 2021-07-14
author: citytwilight
---

# 题目

https://buuoj.cn/challenges#%E4%B8%A2%E5%A4%B1%E7%9A%84MD5



# 解题过程

#### step1：分析

题目给的是一段python代码，解决print语句报错后，发现错误

```
 m.update('TASC'+chr(i)+'O3RJMV'+chr(j)+'WDJKX'+chr(k)+'ZM')
TypeError: Unicode-objects must be encoded before hashing
Unicode 对象必须在hash之前编码
```



#### step2：脚本解密

```
import hashlib   
for i in range(32,127):
    for j in range(32,127):
        for k in range(32,127):
            m=hashlib.md5()
            s='TASC'+chr(i)+'O3RJMV'+chr(j)+'WDJKX'+chr(k)+'ZM'
            m.update(s.encode("utf8"))
            des=m.hexdigest()
            if 'e9032' in des and 'da' in des and '911513' in des:
                print(des)
```

#### step3：得到flag

```
e9032994dabac08080091151380478a2
```



# 问题

```
python 运行的脚本一直出现这个报错“TypeError: Unicode-objects must be encoded before hashing”，知道字符串要先 encode 编码，但是尝试了挺多方法还没解决这个报错

解决：看别人wp的代码思考
```



# 思考总结

代码能力有待提高，包括阅读代码、写代码能力以及找bug



多练习，多看，多思考。

