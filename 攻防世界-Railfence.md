---
layout: post
title: "攻防世界,Railfence"
categories: crypto
tags: 栅栏密码
excerpt: 攻防世界做题的wp，本文章关于栅栏密码。
data: 2021-07-21
author: citytwilight
---



# 题目

https://adworld.xctf.org.cn/task/answer?type=crypto&number=5&grade=0&id=5112&page=1



## 题目类型

```
W型栅栏密码
```



# 解题过程

#### step1：分析

Railfence，即栅栏密码，题目中有5只小鸡，明确栏数是5，然后解密

```
cyperrocae{gireeol}eahfocec_gnbip_g
```

手动分析，利用前几个字母已知(cyberpeace{.+})的条件分析了半天，无果。

查找发现是栅栏密码的变种，WWW型加密https://blog.csdn.net/qinying001/article/details/96134356

```
传统型：
假如有一个字符串：123456789
取字符串长度的因数进行分组，假如key=3
1 2 3  \\分组情况，每三个数字一组，分为三组
4 5 6
7 8 9
然后每一组依次取一个数字组成一个新字符串：147258369 \\加密完成的字符串
=========
WWW型
同样一个字符串：123456789Bkey=3
1 . . . 5 . . . 9     ↘　　　　 　 ↗ ↘             ↗
. 2 . 4 . 6 . 8 .　　　　↘　　   ↗      ↘　      ↗
. . 3 . . . 7 . .     　　 ↘ ↗           ↘　↗         \\让数字以W型组织，同样是三组，但每组的数量不一定相同
加密密文：159246837
```



#### step2：解密

W型栅栏密码，栏数为5

法1：在线网站解密：http://www.atoolbox.net/Tool.php?Id=777

法2：脚本解密

```
def generate_w(string, n):
    array = [['.'] * len(string) for i in range(n)]  # 生成初始矩阵
    row = 0
    upflag = False
    for col in range(len(string)):  # 在矩阵上按w型画出string
        array[row][col] = string[col]
        if row == n - 1:
            upflag = True
        if row == 0:
            upflag = False
        if upflag:
            row -= 1
        else:
            row += 1
    return array


def decode(string, n):
    array = generate_w(string, n)
    sub = 0
    for row in range(n):  # 将w型字符按行的顺序依次替换为string
        for col in range(len(string)):
            if array[row][col] != '.':
                array[row][col] = string[sub]
                sub += 1
    msg = []
    for col in range(len(string)):  # 以列的顺序依次连接各字符
        for row in range(n):
            if array[row][col] != '.':
                msg.append(array[row][col])
    return array, msg


def crack_cipher(string):
    for n in range(2, len(string)):  # 遍历所有可能的栏数
        print(str(n) + '栏：' + ''.join(decode(string, n)[1]))


if __name__ == "__main__":
    string = "ccehgyaefnpeoobe{lcirg}epriec_ora_g"
    crack_cipher(string)
```



#### step3：得到flag

```
cyberpeace{railfence_cipher_gogogo}
```



# 思考总结

普通形式栅栏解密无果后，懵了。栅栏密码的变种W型。这种脑洞是有点，不知道是真的没办法解决



1.对古典密码的了解上还不够，遇到不是很常见的就有点懵

2.解题脚本借鉴的比较多，没怎么进行改进



解决：整理刷题遇到的奇奇怪怪的古典密码吧

