## 递归的拆解

一个`大问题`如何拆解为若干个`小问题`去解决。

例子：

Python:

```py
leftDepth = maxDepth(root.left)
rightDepth = maxDepth(root.right)

return max(leftDepth, rightDepth) + 1
```

整棵树的最大深度，可以拆解为先计算左右子树深度，然后在左右子树深度中找到最大值+1来解决。

Python:

```py
result.append(root)
preorder(root.left, result)
preorder(root.right, result)
```

一棵树的前序遍历可以拆解为3个部分：

1. 根节点自己（root）
2. 左子树的前序遍历
3. 右子树的前序遍历

所以对应的，我们把这个递归问题也拆分为三个部分来解决：

1. 先把 root 放到 result 里 --&gt; result.add\(root\);
2. 再把左子树的前序遍历放到 result 里 --&gt;preorder\(root.left, result\)。回想一下递归的定义，是不是正是如此？
3. 再把右子树的前序遍历放到 result 里 --&gt;preorder\(root.right, result\)。 



