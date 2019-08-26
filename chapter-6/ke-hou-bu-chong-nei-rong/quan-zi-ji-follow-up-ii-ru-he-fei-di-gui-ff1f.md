## 全子集 Follow up II: 如何非递归？

用非递归（Non-recursion / Iteration）的方式实现全子集问题，有两种方式：

1. 进制转换（binary）
2. 宽度优先搜索（Breadth-first Search）

### 进制转换的方法

九章微课堂 - 《位运算入门》 中有此方法的详细讲解：  
[http://www.jiuzhang.com/tutorial/bit-manipulation/83](http://www.jiuzhang.com/tutorial/bit-manipulation/83)

参考代码如下：

Python:

```py
class Solution:
    def subsets(self, nums):
        result = []
        n = len(nums)
        nums.sort()

        # 1 << n is 2^n
        # each subset equals to an binary integer between 0 .. 2^n - 1
        # 0 -> 000 -> []
        # 1 -> 001 -> [1]
        # 2 -> 010 -> [2]
        # ..
        # 7 -> 111 -> [1,2,3]
        for i in range(1 << n):
            subset = []
            for j in range(n):
                if (i & (1 << j)) != 0:
                    subset.append(nums[j])
            result.append(subset)
        return result
```



