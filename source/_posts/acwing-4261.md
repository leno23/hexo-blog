---
title: acwing 4261. 孤独的照片
index_img: https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e42bc36c123847c5b40f3cdaba9af06b~tplv-k3u1fbpfcp-watermark.image
tags: [乘法原理]
categories: [AcWing,算法]
comment: 'valine'
---


4261. 孤独的照片
 

Farmer John 最近购入了 N 头新的奶牛，每头奶牛的品种是更赛牛（Guernsey）或荷斯坦牛（Holstein）之一。

奶牛目前排成一排，Farmer John 想要为每个连续不少于三头奶牛的序列拍摄一张照片。

然而，他不想拍摄这样的照片，其中只有一头牛的品种是更赛牛，或者只有一头牛的品种是荷斯坦牛——他认为这头奇特的牛会感到孤立和不自然。

在为每个连续不少于三头奶牛的序列拍摄了一张照片后，他把所有「孤独的」照片，即其中只有一头更赛牛或荷斯坦奶牛的照片，都扔掉了。

给定奶牛的排列方式，请帮助 Farmer John 求出他会扔掉多少张孤独的照片。

如果两张照片以不同位置的奶牛开始或结束，则认为它们是不同的。

输入格式

输入的第一行包含 N。

输入的第二行包含一个长为 N 的字符串。如果队伍中的第 i 头奶牛是更赛牛，则字符串的第 i 个字符为 G。否则，第 i 头奶牛是荷斯坦牛，该字符为 H。

输出格式

输出 Farmer John 会扔掉的孤独的照片数量。
```
数据范围
3≤N≤5×105
输入样例：
5
GHGHG
输出样例：
3
样例解释
这个例子中的每一个长为 3 的子串均恰好包含一头更赛牛或荷斯坦牛——所以这些子串表示孤独的照片，并会被 Farmer John 扔掉。

所有更长的子串（GHGH、HGHG 和 GHGHG）都可以被接受。
```
[原题链接](https://www.acwing.com/problem/content/description/4264/)

```py

''' 题意计算只含有GH字母的字符串中，长度大于等于3的只含有一个G或者H的子连续子串的个数

# 思路 统计每个位置左右两边和当前字母不相同的连续字母的长度

-xxxxxGxxxxxH
如上，如果G左右两边的H的数量为3和5，这三种情况的子串时满足题意的
1.子串起始部分在G左边，结尾在G右边  
2.子串都在G左边
3.子串都在G右边

记l[i] r[i] 为位置G处，左右两边和他不相同的连续字符的个数

第一种情况 可以以任意左边3个H开头和右边5个H结尾，根据乘法原理 个数为3*5
第二种情况 
    由于子串长度至少是3，那么只能以左边倒数第二个以前的H开头，以G结尾，个数为 max(l[i]-1,0) 
    有可能一个位置左边没有与他相同的字符，例如 GHG H处的l[i]为0，此时这种情况不统计，防止l[i]-1=-1导致结果错误，所以取0
第三种情况
    和上一种情况相同，个数为max(r[i]-1,0)

'''

n=int(input())
s=input()

n=len(s)

# 位置i左右两边与它不相同的连续字符数
l,r=[0]*n,[0]*n

# 前i-1位置中HG的个数
h,g=0,0
for i in range(n):
    if s[i]=='G':
        # 当前字符是G，他左边和他不相同的字符就是h，所以赋值h的个数
        l[i] = h
        # 出现和h不相同的字符，不连续了，h重新计数
        h=0
        # 更新字符G的数目
        g+=1
    else:
        l[i]=g
        g=0
        h+=1
h,g=0,0
# 倒序统计每个位置右边和它不相同的字符的数量
for i in range(n-1,-1,-1):
    if s[i]=='G':
        r[i] = h
        h=0
        g+=1
    else:
        r[i]=g
        g=0
        h+=1
res=0
for i in range(n):
    # 每个位置三种情况的字符数相加
    res += l[i]*r[i] + max(l[i]-1,0)+max(r[i]-1,0)
print(res)
```  