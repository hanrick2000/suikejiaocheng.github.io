## 双指针的鼻祖：两数之和

### 题目描述

给一个整数数组，找到两个数使得他们的和等于一个给定的数 target。  
返回这两个数。

### 使用哈希表来解决

Python:

```py
def twoSum(numbers, target):
    hash_set = set()

    for i in range(len(numbers)):
        if target-numbers[i] in hash_set:
            return (numbers[i], target-numbers[i])
        hash_set.add(numbers[i])

    return None
```

我们使用一个HashSet，来记录每个值是否存在。  
每次查找 target - numbers\[i\] 是否存在，存在即说明找到了，返回两个数即可。

### 使用双指针算法来解决

Python:

```py
class Solution:
    def twoSum(self, numbers, target):
        numbers.sort()

        L, R = 0, len(numbers)-1
        while L < R:
            if numbers[L]+numbers[R] == target:
                return (numbers[L], numbers[R])
            if numbers[L]+numbers[R] < target:
                L += 1
            else:
                R -= 1
        return None
```

  




