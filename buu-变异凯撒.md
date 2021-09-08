---
layout: post
title: "buu,变异凯撒"
categories: crypto python
tags: 凯撒密码 buu
excerpt: buu做题的wp，本文章关于凯撒密码。
data: 2021-07-14
author: citytwilight
---

# 题目

https://buuoj.cn/challenges#%E5%8F%98%E5%BC%82%E5%87%AF%E6%92%92



# 解题过程

#### step1：分析

1.题目提示了，肯定要从凯撒密码入手，先丢到凯撒密码解密试试

```
afZ_r9VYfScOeO_UL^RWUc
bgA_s9WZgTdPfP_VM^SXVd
chB_t9XAhUeQgQ_WN^TYWe
diC_u9YBiVfRhR_XO^UZXf
ejD_v9ZCjWgSiS_YP^VAYg
fkE_w9ADkXhTjT_ZQ^WBZh
glF_x9BElYiUkU_AR^XCAi
hmG_y9CFmZjVlV_BS^YDBj
inH_z9DGnAkWmW_CT^ZECk
joI_a9EHoBlXnX_DU^AFDl
kpJ_b9FIpCmYoY_EV^BGEm
lqK_c9GJqDnZpZ_FW^CHFn
mrL_d9HKrEoAqA_GX^DIGo
nsM_e9ILsFpBrB_HY^EJHp
otN_f9JMtGqCsC_IZ^FKIq
puO_g9KNuHrDtD_JA^GLJr
qvP_h9LOvIsEuE_KB^HMKs
rwQ_i9MPwJtFvF_LC^INLt
sxR_j9NQxKuGwG_MD^JOMu
tyS_k9ORyLvHxH_NE^KPNv
uzT_l9PSzMwIyI_OF^LQOw
vaU_m9QTaNxJzJ_PG^MRPx
wbV_n9RUbOyKaK_QH^NSQy
xcW_o9SVcPzLbL_RI^OTRz
ydX_p9TWdQaMcM_SJ^PUSa
zeY_q9UXeRbNdN_TK^QVTb
```

没有发现什么有用的信息。

2.发现这个下划线貌似代表将密文进行了分割,根据凯撒密码原理，对特殊符号是不移位的，这里有两类特殊符号_ 和 ^  分析 这两个特殊符号的作用，题目既然告诉你是变异凯撒，那么这两个特殊符合就是变异的关键

继续分析，根据特殊符合分割，可以分为4段

```
第一段 ：  afZ

第二段：r9VYfScOeO

第三段：UL

第四段：RWUc
```

可以看到4段都有大小写字符，能不能将大写一组，小写一组，然后解密呢？

```
大写一组：ZVYSOOULRWU

小写一组：afr9fcec
```

尝试解密:没有发现有价值的线索

3.根据凯撒密码原理，对特殊符号是不移位的，特殊符号_ 和 ^  ，尝试从ASCII码入手97 102  90  95  114  57 86  89  102   83  99  79  101  79  95。

```
97+5 = 102  f

102+6=108   l

90+7= 97    a

95+8=103    g
```

于是发现是按顺序从5开始从每个递增加上1。



#### step2：脚本解密

```
str = "afZ_r9VYfScOeO_UL^RWUc"
i = 5
flag = ""
for s in str:
    flag += chr(ord(s) + i)
    i += 1
print(flag)
```

注：

```
ord(字符串) 返回值为int
chr(数值表达式) 返回值为string 数值表达式取值范围0~255
```



#### step3：得到flag

```
flag{Caesar_variation}
```



# 问题

```
一：知道是凯撒密码变种，但是没想到底是什么样的变种

解决：经过分析和别人wp得到了思路

二：有了思路后，编写脚本的问题

解决：结合别人脚本代码，思考理解吸收
```



# 思考总结

看见题目是变异凯撒，立即与凯撒密码联系起来，但是在凯撒失败（毕竟是变异凯撒，不可能直接凯撒就出结果）后，不知道改怎么分析了



角度这种东西就是看自己脑洞了。想不到只能到别人wp中找思路
