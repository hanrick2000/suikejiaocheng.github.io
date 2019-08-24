## 递归的定义

每一个递归函数，都需要有明确的定义，有了正确的定义以后，才能够对递归进行拆解。

例子：  
Python:

```py
def maxDepth(root):
```

代表`以 root 开头的子树的最大深度是多少`。  


Python:

```py
def preorder(root, result):
```

代表`将 root 开头的子树的前序遍历放到 result 里面`

