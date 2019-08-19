## 判断回文串

另外一个双指针的经典练习题，就是回文串的判断问题。给一个字符串，判断这个字符串是不是回文串。

我们可以用双指针的算法轻易的解决：

Python:

```py
def isPalindrome(s):
    i, j = 0, len(s)-1
    while i < j:
        if s[i] != s[j]:
            return False
        i += 1
        j -= 1
    return True
```

### Follow up 1: 不区分大小写，忽略非英文字母

完整的题目描述请见：  
[http://www.lintcode.com/problem/valid-palindrome/](http://www.lintcode.com/problem/valid-palindrome/)

这个问题本身没有太大难度，只是为了给过于简单的 isPalindrome 函数增加一些实现技巧罢了。  
代码上和上面的 isPalindrome 函数主要有2个区别：

1. 在 i++ 和 j-- 的时候，要用 while 循环不断的跳过非英文字母
2. 比较的时候要都变成小写之后再比较

[参考答案](http://www.jiuzhang.com/solution/valid-palindrome/)

### Follow up 2: 允许删掉一个字母（类似的，允许插入一个字母）

完整的题目描述请见：  
[http://www.lintcode.com/problem/valid-palindrome-ii/](http://www.lintcode.com/problem/valid-palindrome-ii/)

FLAG 的面经中出现过此题。一个简单直观的粗暴想法是，既然要删除一个字母，那么我们就 for 循环枚举（Enumerate）每个字母，试试看删掉这个字母之后，该字符串是否为一个回文串。

上述粗暴算法的时间复杂度是 $$O(n^2)$$，因为 for 循环枚举被删除字母的复杂度为$$O(n)$$，判断剩余字符构成的字符串是否为回文串的复杂度为$$O(n)$$，总共花费$$O(n^2)$$。这显然一猜就应该不符合面试官的要求。

正确的算法如下：

1. 依然用相向双指针的方式从两头出发，两根指针设为 L 和 R。
2. 如果 s\[L\] 和 s\[R\] 相同的话，L++, R--
3. 如果 s\[L\] 和 s\[R\] 不同的话，停下来，此时可以证明，如果能够通过删除一个字符使得整个字符串变成回文串的话，那么一定要么是 s\[L\]，要么是 s\[R\]。

简单的来说，这个算法就是依然按照原来的算法走一遍，然后碰到不一样的字符的时候，从总选一个删除，如果删除之后的字符换可以是 Palindrome 那就可以，都不行的话，那就不行。

这个需要一点数学证明来证明为什么是对的，大家可以先尝试自己证明一下，再来看下面的答案：

[证明 ](https://www.jiuzhang.com/tutorial/algorithm/390#collapse1)

  


