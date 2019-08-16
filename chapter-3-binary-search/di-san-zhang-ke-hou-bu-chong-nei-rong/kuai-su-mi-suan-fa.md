## 快速幂算法

### 基本原理

计算x的n次方， 即计算$$x^n$$。

由公式可知： $$x^n = x^{n/2} * x^{n/2}$$。

如果我们求得 $$x^{n/2}$$， 则可以O\(1\)求出x^n, 而不需要再去循环剩下的n/2次。

以此类推，若求得 $$x^{n/4}$$， 则可以O\(1\)求出 $$x^{n/2}$$。  
。。。

因此一个原本O\(n\)的问题，我们可以用O\(logn\)复杂度的算法来解决。

### 递归版本的快速幂算法

Python:

```py
def power(x, n):
    if n == 0:
        return 1

    if n % 2 == 0:
        tmp = power(x, n // 2)
        return tmp * tmp
    else:
        tmp = power(x, n // 2)
        return tmp * tmp * x
```

注意:

* 不要重复计算，在计算 $$x^{n/2} * x^{n/2}$$的时候，先计算出 $$x^{n/2}$$，存下来然后返回 $$tmp*tmp$$;
* n为奇数的时候要记得再乘上一个x。

### 非递归版本

Python:

```py
def power(x, n):
    ans = 1
    base = x
    while n > 0:
        if n % 2 == 1:
            ans *= base
        base *= base
        n = n // 2
    return ans
```

非递归版本与递归版本原理相同，计算顺序略有不同。

因为递归是从大问题进入，划分子问题然后层层返回再求解大问题。这里要从小问题开始，直接求解大问题。  
你可以打印出每次循环中base和ans的值，来理清楚其中的算法思路。

递归版本和非递归版本都应该熟练掌握，虽然递归版本更容易掌握和理解，且logn的计算深度也不会导致 Stack Overflow。但是面试官是很有可能为了加大难度让你在用非递归的版本写一遍的。

### 相关练习

[http://www.lintcode.com/problem/fast-power/](http://www.lintcode.com/problem/fast-power/)  
[http://www.lintcode.com/problem/powx-n/](http://www.lintcode.com/problem/powx-n/)

