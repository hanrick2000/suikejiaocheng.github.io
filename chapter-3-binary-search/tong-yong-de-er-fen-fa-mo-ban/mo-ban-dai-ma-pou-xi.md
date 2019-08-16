## 模板代码剖析

其他语言的参考代码请见：  
[http://www.jiuzhang.com/solutions/binary-search/  
](http://www.jiuzhang.com/solutions/binary-search/)

### 常见问题

**Q: 为什么要用 start + 1 &lt; end？而不是 start &lt; end 或者 start &lt;= end？**

A: 为了避免死循环。二分法的模板中，整个程序架构分为两个部分：

1. 通过 while 循环，将区间范围从 n 缩小到 2 （只有 start 和 end 两个点）。
2. 在 start 和 end 中判断是否有解。

start &lt; end 或者 start &lt;= end 在寻找目标最后一次出现的位置的时候，出现死循环。

**Q: 为什么明明可以 start = mid + 1 偏偏要写成 start = mid?**

A: 大部分时候，mid 是可以 +1 和 -1 的。在一些特殊情况下，比如寻找目标的最后一次出现的位置时，当 target 与 nums\[mid\] 相等的时候，是不能够使用 mid + 1 或者 mid - 1 的。因为会导致漏掉解。那么为了节省`脑力`，统一写成 start = mid / end = mid 并不会造成任何解的丢失，并且也不会损失效率——log\(n\) 和 log\(n+1\) 没有区别。



