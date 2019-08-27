## 堆化 Heapify

[完整参考代码](http://www.jiuzhang.com/solution/heapify/)

### 基于 Siftup 的版本O\(nlogn\)

Python版本：

```py
import sys
import collections
class Solution:
    # @param A: Given an integer array
    # @return: void
    def  siftup(self, A, k):
        while k != 0:
            father = (k - 1) // 2
            if A[k] > A[father]:
                break
            temp = A[k]
            A[k] = A[father]
            A[father] = temp
            
            k = father
    def heapify(self, A):
        for i in range(len(A)):
            self.siftup(A, i)
```

**算法思路：**

1. 对于每个元素A\[i\]，比较A\[i\]和它的父亲结点的大小，如果小于父亲结点，则与父亲结点交换。
2. 交换后再和新的父亲比较，重复上述操作，直至该点的值大于父亲。

#### 时间复杂度分析

1. 对于每个元素都要遍历一遍，这部分是O\(n\)。
2. 每处理一个元素时，最多需要向根部方向交换
   logn
   l
   o
   g
   n
   次。

因此总的时间复杂度是O\(nlogn\)O\(nlogn\)

  


