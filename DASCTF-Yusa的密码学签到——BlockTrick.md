---
layout: post
title: "DASCTF,Yusa的密码学签到——BlockTrick"
categories: crypto python
tags: nc连接 
excerpt: DASCTF比赛做题的wp，本文章关于crypto。
data: 2021-08-01
author: citytwilight
---

# 题目

https://buuoj.cn/plugins/ctfd-matches/matches/15/challenges



# 解题过程

#### step1：ubuntu nc连接

nc连接命令

```
nc node4.buuoj.cn 27460
```

得到

```
59514b0322724498884c0c592b7c2c67
```

#### step2：查看代码

```
from Crypto.Cipher import AES
import os

from past.builtins import raw_input


def pad(a):
    size = (16 - len(a) % 16) % 16
    a += chr(size) * size
    return a


iv = os.urandom(16)
key = os.urandom(16)
enc = AES.new(key, AES.MODE_CBC, iv)
print(iv.encode('hex'))

for _ in range(2):
    try:
        trick = raw_input("")
        trick = pad(trick.decode('hex'))
        cipher = enc.encrypt(trick)
        if trick == cipher and trick != "":
            with open("flag.txt") as f:
                print(f.read())
                exit()
        else:
            print(cipher.encode('hex'))
            print("Try again")
    except:
        exit()

```

可以看出，nc连接得到的是trick 输入trick得到cipher

```
62a6c8e42b7b16a02fb22f29af4157a9
```

返回Try again

接着根据代码提示 可知，输入cipher，当cipher=trick时返回flag



#### step3：返回flag

```
flag{630f4766-26d2-4280-84b3-fcee0871ec56}
```



# 思考总结

接触的题目还是太少了，nc连接都不知道，一度以为自己靶机连不上

解决：向学姐请教了、百度相关命令



收获：见识了大赛的题目，跟平时刷的题差距挺大的，感觉是综合应用。

需要走的路还很长，继续加油

