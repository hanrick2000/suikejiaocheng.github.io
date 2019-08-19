## 三指针算法

### 题目描述

将包含0，1，2三种颜色代码的数组按照颜色代码的大小排序。如`[1,0,1,0,2]`=&gt;`[0,0,1,1,2]`。

LintCode 提交地址：[http://www.lintcode.com/problem/sort-colors/](http://www.lintcode.com/problem/sort-colors/)

### 解法分析

在颜色排序（Sort Color）这个问题中，传统的双指针算法可以这么做：

1. 先用 partition 的方式区分开 0 和 1, 2
2. 再在右半部分区分开 1 和 2

这个算法不可避免的要使用两次 Parition，写两个循环。许多面试官会要求你，能否只 partition 一次，也就是只用一个循环。

用一个循环的方法如下：

[http://www.jiuzhang.com/solution/sort-colors](http://www.jiuzhang.com/solution/sort-colors)

分析一下核心代码部分：

Python:

```

```





