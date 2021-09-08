---
layout: post
title: "buu,wireshark"
categories: misc
tags: wireshark buu
excerpt: buu做题的wp，本文章wireshark。
data: 2021-07-17
author: citytwilight
---

# 题目

https://buuoj.cn/challenges#wireshark

# 解题过程

#### step1：把这个PCAP文件拖到wireshark打开

![](D:\桌面\刷题\markdown\图片\7.png)

#### step2：由于在网站登录,于是试着找出http协议的包，发现有login信息，追踪http流

![](D:\桌面\刷题\markdown\图片\8.png)

#### step3：追踪后查找关键字flag

![](D:\桌面\刷题\markdown\图片\9.png)

#### step4：发现password

![](D:\桌面\刷题\markdown\图片\10.png)

step5：得出flag

```
ffb7567a1d4f4abdffdb54e022f8facd
```



# 问题

```
wireshark使用不熟练

解决：查看使用教程，多进行抓包分析
```



# 思考总结

对工具的使用还是太少，不够熟练，对misc方向也是，知识储备太少，不知道怎么下手
