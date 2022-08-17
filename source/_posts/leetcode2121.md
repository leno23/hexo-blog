---
title: Leetcode 2121. 相同元素的间隔之和
index_img: https://rmt.dogedoge.com/fetch/fluid/storage/bg/n7a9bv.png?w=1920&fmt=webp
banner_img: https://rmt.dogedoge.com/fetch/fluid/storage/bg/n7a9bv.png?w=1920&fmt=webp
tags: [模拟]
---

今天我们来做一下今天的leetcode上一道中等题

题目链接在这里#### [2121. 相同元素的间隔之和](https://leetcode.cn/problems/intervals-between-identical-elements/)

### 题意

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c1b96c52e02e433795360200d051c104~tplv-k3u1fbpfcp-watermark.image?)
题目给了我们了一个数组，让我们求其中的一个数字和其他所有位置的相同数字的间隔之和。
什么意思呢？ 假如这个数组是  2 1 3 1 2 3 3 
求下标为2的数字3的间隔之和，就等于它和其他两个3的距离之和，也就是 等于 3 + 4 = 7
其他的每个数字都按照这个方法进行计算

### 思路

这道题读过题之后，感觉比较简单，但是一下子又想不到好的代码实现思路，这是我第一次做这道题的情景。😪

不过，还好后面坚持思考了一下，才明白一种解决的办法。话不多说，直接上图。
![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bbeb4d2091e84ee497defd343c640c1a~tplv-k3u1fbpfcp-watermark.image?)

- 如上图所示，我们想要计算每一个3的间隔总和，首先我们可以统计出来3的所有位置信息，也就是2 5 6 7
- 然后，我们可以统计出来每个数字都出现在哪些位置了。之后，我们就可以开始计算间隔和了
- 我们发现第一个3的间隔总和比较好算，也就是从第2个3开始遍历后面的5 6 7，将他们和2的距离相加求和即可。
- 我们紧接着考虑计算第二个3的间隔总和，首先，把5和每个数（包含自己）的间隔画出来的话，就像图中那，在把2和每个数的间隔也画出来。从2的每个间隔 到 5的每个间隔 我们可以发现，左侧有一个间隔增加了 5-2，右侧三个间隔减少了5-2，增加和减少的间隔分别对应红色和绿色标注的线段；
    - 继续，再观察5到6的变化，可以发现，左侧有两个增加了6-5，右侧有两个减少了6-5，。。。
    - 当我们找到这些相邻位置的间隔和的变化规律时，我们可以总结如下
    ```
    假设间隔数组为p，那么，第i个数的间隔和相对于第i-1个数增加了
       = 增加量 - 减少量
       = i*(p[i]-p[i-1]) - (n-i)*(p[i] - p[i-1])
       = (2*i-n)(p[i]-p[i-1])
   ```
至此，我们就找到了计算一个数字的 每个位置的间隔和的规律了。😘

### 代码实现

了解了上面的思路之后，代码实现其实就非常简单了😎。

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7d481b704dbe47c29668505450f42a55~tplv-k3u1fbpfcp-watermark.image?)
### 结束语

如果有更好的分析思路，欢迎大家在评论区发表看法！⛄