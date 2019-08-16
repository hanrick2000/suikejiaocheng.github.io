## 时间复杂度小练习

计算下面这些代码的时间复杂度

### 练习 1

  
Python:

```py
sum = 0
i = 0
while i < n:
    sum += 1
    i *= 2
```

时间复杂度为

O\(logn\)

如果你将 sum 的值打印出来，就可以发现sum=logn\(以2为底\)，说明 for 循环共循环了logn次。



### 练习 2

### Python

```py
sum = 0
for i in range(n):
    j = 1
    while j <= n:
        sum += 1
        j *= 2
```

时间复杂度为

O\(nlogn\)

### 练习 3



Python:

```py
def Fibo(n):
    if n == 0 or n == 1:
        return 1
    return Fibo(n-1) + Fibo(n-2)
```



时间复杂度为  $$O(2^\frac{n}{2})~O(2^n)$$

计算时间复杂度上界：Fibo\(n\) = Fibo\(n-1\) + Fibo\(n-2\) &lt; 2 \* Fibo\(n-1\)Fibo\(n\)=Fibo\(n−1\)+Fibo\(n−2\)&lt;2∗Fibo\(n−1\)  
也就是说，递归版 Fibonacci 的时间复杂度 &lt;T\(n\) = 2 \* T\(n-1\) + O\(1\) = O\(2^n\)T\(n\)=2∗T\(n−1\)+O\(1\)=O\(2n\)

再来计算时间复杂度下界：Fibo\(n\) = Fibo\(n-1\) + Fibo\(n-2\) &gt; 2 \* Fibo\(n-2\)Fibo\(n\)=Fibo\(n−1\)+Fibo\(n−2\)&gt;2∗Fibo\(n−2\)  
也就是说，递归版 Fibonacci 的时间复杂度 &gt;T\(n\) = 2 \* T\(n-2\) + O\(1\) = O\(2^\frac{n}{2}\)T\(n\)=2∗T\(n−2\)+O\(1\)=O\(22n​\)



