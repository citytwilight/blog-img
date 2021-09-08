---
layout: post
title: "buu,传统知识+古典密码"
categories: crypto 
tags: 古典密码 buu
excerpt: buu做题的wp，本文章关于古典密码。
data: 2021-07-16
author: citytwilight6
---

# 题目

https://buuoj.cn/challenges#%E4%BC%A0%E7%BB%9F%E7%9F%A5%E8%AF%86+%E5%8F%A4%E5%85%B8%E5%AF%86%E7%A0%81

# 解题过程

#### step1：分析

传统知识：60甲子年表

| 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 甲子 | 乙丑 | 丙寅 | 丁卯 | 戊辰 | 己巳 | 庚午 | 辛未 | 壬申 | 癸酉 |
| 11   | 12   | 13   | 14   | 15   | 16   | 17   | 18   | 19   | 20   |
| 甲戌 | 乙亥 | 丙子 | 丁丑 | 戊寅 | 己卯 | 庚辰 | 辛巳 | 壬午 | 癸未 |
| 21   | 22   | 23   | 24   | 25   | 26   | 27   | 28   | 29   | 30   |
| 甲申 | 乙酉 | 丙戌 | 丁亥 | 戊子 | 己丑 | 庚寅 | 辛卯 | 壬辰 | 癸巳 |
| 31   | 32   | 33   | 34   | 35   | 36   | 37   | 38   | 39   | 40   |
| 甲午 | 乙未 | 丙申 | 丁酉 | 戊戌 | 己亥 | 庚子 | 辛丑 | 壬寅 | 癸卯 |
| 41   | 42   | 43   | 44   | 45   | 46   | 47   | 48   | 49   | 50   |
| 甲辰 | 乙巳 | 丙午 | 丁未 | 戊申 | 己酉 | 庚戌 | 辛亥 | 壬子 | 癸丑 |
| 51   | 52   | 53   | 54   | 55   | 56   | 57   | 58   | 59   | 60   |
| 甲寅 | 乙卯 | 丙辰 | 丁巳 | 戊午 | 己未 | 庚申 | 辛酉 | 壬戌 | 癸亥 |

step2：对照60甲子年表得出值28 30 23 8 17 10 16 30 结合题目＋甲子（一甲子为60年）得：88 90 83 68 77 70 76 90 就能得到对应的ACSLL字符了 ：XZSDMFLZ（为了方面辨识出有含义的flag，解密使用小写）

古典密码第一反应是凯撒，解密

```
xzsdmflz
yatengma
zbufohnb
acvgpioc
bdwhqjpd
cexirkqe
dfyjslrf
egzktmsg
fhalunth
gibmvoui
hjcnwpvj
ikdoxqwk
jlepyrxl
kmfqzsym
lngratzn
mohsbuao
npitcvbp
oqjudwcq
prkvexdr
qslwfyes
rtmxgzft
sunyhagu
tvozibhv
uwpajciw
vxqbkdjx
wyrcleky
```

好像都没含义，所以尝试先进行栅栏

```
2栏：
xmzfsldz

4栏：
xsmlzdfz
```

再进行凯撒



```
二栏：
xmzfsldz
ynagtmea
zobhunfb
apcivogc
bqdjwphd
crekxqie
dsflyrjf
etgmzskg
fuhnatlh
gviobumi
hwjpcvnj
ixkqdwok
jylrexpl
kzmsfyqm
lantgzrn
mbouhaso
ncpvibtp
odqwjcuq
perxkdvr
qfsylews
rgtzmfxt
shuangyu
tivbohzv
ujwcpiaw
vkxdqjbx
wlyerkcy
```

```
四栏：
xsmlzdfz
ytnmaega
zuonbfhb
avpocgic
bwqpdhjd
cxrqeike
dysrfjlf
eztsgkmg
fauthlnh
gbvuimoi
hcwvjnpj
idxwkoqk
jeyxlprl
kfzymqsm
lgaznrtn
mhbaosuo
nicbptvp
ojdcquwq
pkedrvxr
qlfeswys
rmgftxzt
snhguyau
toihvzbv
upjiwacw
vqkjxbdx
wrlkycey
```

shuangyu比较通顺

step3：得出flag

```
SHUANGYU
```

# 问题

```
一开始看见题目中的年份，；联想到最近的天干地支年份对照表(比如最近的甲子年是1993)

解决：及时调整思路

古典一开始只能想到凯撒，凯撒解密发现没有的时候，不知所措了

解决：尝试先进行其他的古典密码再进行凯撒，比如栅栏。
```



# 思考总结

不能陷入误区，得不出结果的时候要考虑是否是思考的方向角度不对 多进行发散性思维

