---
layout: post
title: "攻防世界,easy_ECC"
categories: crypto python
tags: ECC
excerpt: 攻防世界做题的wp，本文章关于椭圆曲线密码。
data: 2021-07-24
author: citytwilight
---

# 题目

https://adworld.xctf.org.cn/task/answer?type=crypto&number=5&grade=0&id=5116&page=1

## ECC题目类型

```
已知椭圆曲线p、a、b，私钥k，点G
求解公钥
```

已知公钥，求解e,n,p,q，最后通过解密已加密文件，获取flag。

RSA攻击----已知公钥n，e私钥d。

# 解题过程

#### step1：分析

已知椭圆曲线p、a、b，私钥k，点G

#### step:2：解密

法1：工具解密

工具下载地址：https://bbs.pediy.com/thread-66683.htm

![](D:\桌面\刷题\markdown\图片\adasdas.png)

法2：脚本解密

```
import libnum

#通过二进制分解私钥 K 计算公钥
#依次计算 2G，4G，8G 的值，遇到二进制为 1 的位，就进行结果相加例如 11=1G+2G+8G，但是初始值不好确定，所以加入 first 确定第一个初始值
def main(p,a,b,k,x,y):
    str=bin(k)[2:][::-1]
    result_x,result_y=0,0
    first=True
    #初值设置
    if str[0]=='1':
        result_x,result_y=x,y
        first=False
    #从 2G 开始计算
    for i in range(1,len(str),1):
        x,y=compute(x,y,x,y)
        #二进制为 1 则加到结果上
        if(str[i]=='1'):
            #初值判断
            if first:
                result_x,result_y=x,y
                first=False
            #加到结果上
            else:
                result_x,result_y=compute(result_x,result_y,x,y)
    return result_x,result_y

#计算 a/b mod p 的结果
def div(a,b,p):
    #对 b 求逆
    d=libnum.invmod(b,p)
    return a*d%p

#计算(x1,y1)+(x2,y2)的结果
def compute(x1,y1,x2,y2):
    #根据不同情况计算 lamda 的值
    if x1==x2 and y1==y2:
        lamda1=(3*(x2**2)+a)%p
        lamda2=(2*y1)%p
    else:
        lamda1=(y2-y1)%p
        lamda2=(x2-x1)%p

    lamda=div(lamda1,lamda2,p)
    x3=(lamda**2-x1-x2)% p
    y3=(lamda*(x1-x3)-y1)% p

    return x3,y3

if __name__=="__main__":
    p = 15424654874903
    a = 16546484
    b = 4548674875
    k = 546768
    x = 6478678675
    y = 5636379357093
    x,y=main(p,a,b,k,x,y)
    print("公钥 K(%d,%d)"%(x,y))
    print(x + y)
```



#### step3：得到flag

x+y

```
19477226185390
```



# 思考总结

没接触过ECC的题目，但是幸好上学期密码学学的基础知识没忘记，基本原理还是了解的。本意是写脚本解决，但是偶然发现了ECC的一个工具，就收下了。



1. 一开始找的wp的脚本报错，emmm 看了半天不知道是啥问题，就找的另外一个脚本，结合密码学实验课的代码，整出了脚本。
2. 改BUG能力太差了。（一开始那个脚本，看了是没啥问题的，运行正常，中间也符合原理，但是我运行下来得不到预期结果）
