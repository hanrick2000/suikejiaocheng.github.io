## 空间复杂度小练习

写出如下算法的空间复杂度

### 练习 1

  
Python:

```py
def Fibo(n):
    if n == 0 or n == 1:
        return 1
    return Fibo(n-1) + Fibo(n-2)
```

O\(n\)



### 练习 2

Python:

```py
def Fibo(n):
    x1, x2, ret = 1, 1, 1
    for i in range(2, n+1):
        ret = x1 + x2
        x1, x2 = x2, ret
    return ret
```

O\(1\)

