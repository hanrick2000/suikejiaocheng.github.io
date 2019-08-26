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

### 基于 BFS 的方法

在 BFS 那节课的讲解中，我们很少提到用 BFS 来解决找所有的方案的问题。事实上 BFS 也是可以用来做这件事情的。  
用 BFS 来解决该问题时，层级关系如下：

```
第一层: []
第二层: [1] [2] [3]
第三层: [1, 2] [1, 3], [2, 3]
第四层: [1, 2, 3]
```

每一层的节点都是上一层的节点拓展而来。

参考代码如下：  
Python:

```py
lass Solution:
    def subsets(self, nums):
        results = []

        if not nums:
            return results

        nums.sort()

        # BFS
        queue = deque()
        queue.append([])

        while queue:
            subset = queue.popleft()
            results.append(subset)

            for i in range(len(nums)):
                if not subset or subset[-1] < nums[i]:
                    nextSubset = list(subset)
                    nextSubset.append(nums[i])
                    queue.append(nextSubset)

        return results
```



