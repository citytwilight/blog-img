---
layout: post
title: "其他,CaesarPlus"
categories: crypto python
tags: 凯撒密码 
excerpt: 做题的wp，本文章关于凯撒密码。
data: 2021-08-09
author: citytwilight
---

# 题目

```
Z25ka4A7O21AO3BERDtCSEp3QEhFSHpFe01LVUqDU1WFWlddXVhYXV2n
```



# 解题过程

#### step1：分析

1.先尝试进行base64解码

```
gndk;;m@;pDD;BHJw@HEHzE{MKUJSUZW]]XX]](在线网站解密结果)

gndk\x80;;m@;pDD;BHJw@HEHzE{MKUJ\x83SU\x85ZW]]XX]]\xa7(这个是正确解密的结果)
```

2.分析gndk 的ASCII码103 110 100 107，与flag进行对比，发现

```
103 - 1 = 102  f

110 - 2 = 108  l

100 - 3 = 97   a

107 - 4 = 103  g
```

于是发现是按顺序从1开始从每个递减1。



#### step2：脚本解密

```
import base64

str1 = 'Z25ka4A7O21AO3BERDtCSEp3QEhFSHpFe01LVUqDU1WFWlddXVhYXV2n'
str=base64.b64decode(str1.encode())
i = 1
flag = ""
for s in str:
    flag += chr(s - i)
    i += 1
print(flag)
```



#### step3：得到flag

```
flag{54e71e87-389e-402c-b309-e45d84982154}
```



# 思考总结

因为在线网站base64解密结果有不可见字符，导致结果不对



解决：利用python base库解密
