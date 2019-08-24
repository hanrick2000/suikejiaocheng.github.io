## 递归的出口

什么时候可以直接知道答案，不用再拆解，直接 return

例子：

Python:

```py
# 二叉树的最大深度
if not root:
    return 0
```

一棵空的二叉树，可以认为是一个高度为`0`的二叉树。  


Python:

```py
if not root:
    return
```

一棵空的二叉树，自然不用往 result 里放任何的东西。  




