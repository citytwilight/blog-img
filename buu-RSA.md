---
layout: post
title: "buu,RSA"
categories: crypto python
tags: RSA buu
excerpt: buu做题的wp，本文章关于RSA。
data: 2021-07-13
author: citytwilight
---

# 题目

https://buuoj.cn/challenges#RSA



#### RSA题目类型

	已知公钥，求解e,n,p,q，最后通过解密已加密文件，获取flag。
	
	RSA攻击----已知公钥n，e私钥d。

#### 包含

	flag.enc
	
	pub.key



# 题解过程

#### **step1：通过pub.key求解e,n,p,q。**

​	直接通过解密网站求解：http://tool.chacuo.net/cryptrsakeyparse（公私钥分解参数）

​	求得：

| key：  | 256                                                          |
| :----- | ------------------------------------------------------------ |
| 模数： | C0332C5C64AE47182F6C1C876D42336910545A58F7EEFEFC0BCAAF5AF341CCDD |
| 指数： | 65537 (0x10001)                                              |

​	上表格e为：e = 65537(十进制)

​	然后将模数进行进制转换：16进制转换成10进制。https://tool.lu/hexconvert/ (进制转换)

```
	e = 65537

	n = 86934482296048119190666062003494800588905656017203025617216654058378322103517

```



#### **step2：提取p，q。**

法1：直接通过解密网站进行求解：http://www.factordb.com/index.php?query= （大素数分解）

```
	
	p = 285960468890451637935629440372639283459
	
	q = 304008741604601924494328155975272418463
```

法2：使用yafu进行大素数分解

```
D:\桌面\ctf-crypto\工具\yafu-1.34>yafu-x64.exe
factor(86934482296048119190666062003494800588905656017203025617216654058378322103517)


fac: factoring 86934482296048119190666062003494800588905656017203025617216654058378322103517
fac: using pretesting plan: normal
fac: no tune info: using qs/gnfs crossover of 95 digits

starting SIQS on c77: 86934482296048119190666062003494800588905656017203025617216654058378322103517

==== sieving in progress (1 thread):   36224 relations needed ====
====           Press ctrl-c to abort and save state           ====


SIQS elapsed time = 1.2452 seconds.
Total factoring time = 1.3531 seconds


***factors found***

P39 = 304008741604601924494328155975272418463
P39 = 285960468890451637935629440372639283459

ans = 1
```



#### **step3：脚本解密。**

```
import rsa
import gmpy2

p = 285960468890451637935629440372639283459
q = 304008741604601924494328155975272418463
e = 65537
n = 86934482296048119190666062003494800588905656017203025617216654058378322103517

d = gmpy2.invert(e, (p - 1) * (q - 1))

key = rsa.PrivateKey(n, e, int(d), q, p)
with open("D:\\桌面\\刷题\\题目\\RSA\\flag.enc", "rb") as f:
    f = f.read()
    print(rsa.decrypt(f, key))

```



#### **step4：得到flag。**


	flag{decrypt_256}






# 遇到问题

	一：含中文的路径编译时会报错。
	
	解决：
	
	1. 改成英文路径。
	
	2. 原来的“\”改为“\\”
	
	二：key = rsa.PrivateKey(n, e, d, q, p)会报错
	
	解决：将d强制转换为int类型
	
	三：大数的进制转换，一开始尝试用python自带的进制转换(但是取值突破上限了)
	
	解决：找的网站进行进制转换(后期自己写个进制转换的脚本)



# 总结思考

由于没接触RSA包含flag.enc、pub.key类型的题目，一时间不知道怎么下手，最后参考学姐的wp和网上的wp找到思路，进行脚本解密。https://www.cnblogs.com/harmonica11/p/11504291.html



1.完全没接触过这种类型的RSA题目

2.不会调用脚本模块里的函数
