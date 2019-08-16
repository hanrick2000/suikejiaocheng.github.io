## 为什么 start &lt; end 容易出现死循环

许多同学在写二分法的时候，都比较习惯性的写`while (start < end)`这样的循环条件。这样的写法及其容易出现死循环，导致 LintCode 上的测试“超时”（Time Limit Exceeded）。

#### 什么情况下会出现死循环？

在做`last position of target`这种模型下的二分法时，使用 while \(start &lt; end\) 就容易出现超时。

在线练习：  
[http://www.lintcode.com/problem/last-position-of-target/](http://www.lintcode.com/problem/last-position-of-target/)

我们来看看会超时的代码：

Python版本：

```py
start, end = 0, len(nums) - 1
while start <end:
    mid = start + (end - start) // 2
    if nums[mid] == target:
        start = mid
    else if nums[mid] < target:
        start = mid + 1
    else:
        end = mid - 1
```





  
上面这份代码是大部分同学的实现方式。看上去似乎没有太大问题。我们来注意一下 \`nums\[mid\] == target\` 时候的处理。这个时候，因为 mid 这个位置上的数有可能是最后一个出现的target，所以不能写成 start = mid + 1（那样就跳过了正确解）。而如果是这样写的话，下面这组数据将出现超时\(TLE\)：

```
nums = [1,1], target = 1
```

将数据带入过一下代码：  


```
start = 0, end = 1
while (0 < 1) {
mid = 0 + (1 - 0) / 2 = 0
if (nums[0] == 1) {
start = 0;
}
...
}
```



我们发现，start 将始终是 \`0\`。

出现这个问题的主要原因是，mid = start + \(end - start\) / 2 这种写法是偏向start的。也就是说 mid 是中间偏左的位置。这样导致如果 start 和 end 已经是相邻关系，会导致 start 有可能在一轮循环之后保持不变。



或许你会说，那么我改成 mid = \(start + end + 1\) / 2 是否能解决问题呢？没错，确实可以解决 last position of target 的问题，但是这样之后 first position of target 就超时了。我们比较希望能够有一个理想的模板，无论是 first position of target 还是 last position of target，代码的区别尽可能的小和容易记住。





