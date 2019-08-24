## 非递归的方式实现二叉树遍历

### 先序遍历

#### 思路

遍历顺序为**根**、**左**、**右**

1. 如果根节点非空，将根节点加入到栈中。
2. 如果栈不空，弹出出栈顶节点，将其值加加入到数组中。
   1. 如果该节点的右子树不为空，将右子节点加入栈中。
   2. 如果左子节点不为空，将左子节点加入栈中。
3. 重复第二步，直到栈空。

#### 代码实现

Python:

```py
class Solution:
    """
    @param root: A Tree
    @return: Preorder in ArrayList which contains node values.
    """
    def preorderTraversal(self, root):
        stack = []
        preorder = []

        if not root:
            return preorder

        stack.append(root)
        while len(stack) > 0:
            node = stack.pop()
            preorder.append(node.val)
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        
        return preorder
```

#### 练习

[http://www.lintcode.com/problem/binary-tree-preorder-traversal/](http://www.lintcode.com/problem/binary-tree-preorder-traversal/)

### 中序遍历

#### 思路

遍历顺序为**左**、**根**、**右**

1. 如果根节点非空，将根节点加入到栈中。
2. 如果栈不空，取栈顶元素（暂时不弹出），
   1. 如果左子树已访问过，或者左子树为空，则弹出栈顶节点，将其值加入数组，如有右子树，将右子节点加入栈中。
   2. 如果左子树不为空，则将左子节点加入栈中。
3. 重复第二步，直到栈空。

#### 代码实现

Python

```py
class Solution:
    """
    @param root: A Tree
    @return: Inorder in ArrayList which contains node values.
    """
    def inorderTraversal(self, root):
        stack = []
        result = []

        while root:
            stack.append(root)
            root = root.left

        while len(stack) > 0:
            node = stack[-1]
            result.append(node.val)

            if not node.right:
                node = stack.pop()
                while len(stack) > 0 and stack[-1].right == node:
                    node = stack.pop()
            else:
                node = node.right
                while node:
                    stack.append(node)
                    node = node.left
        
        return result

```

#### 练习

[http://www.lintcode.com/problem/binary-tree-inorder-traversal/](http://www.lintcode.com/problem/binary-tree-inorder-traversal/)

### 后序遍历

#### 思路

遍历顺序为**左**、**右**、**根**

1. 如果根节点非空，将根节点加入到栈中。
2. 如果栈不空，取栈顶元素（暂时不弹出），
   1. 如果（左子树已访问过或者左子树为空），且（右子树已访问过或右子树为空），则弹出栈顶节点，将其值加入数组，
   2. 如果左子树不为空，切未访问过，则将左子节点加入栈中，并标左子树已访问过。
   3. 如果右子树不为空，切未访问过，则将右子节点加入栈中，并标右子树已访问过。
3. 重复第二步，直到栈空。

#### 代码实现

Python

```py
class Solution:
    """
    @param root: A Tree
    @return: Postorder in ArrayList which contains node values.
    """
    def postorderTraversal(self, root):
        result = []
        stack = []
        prev, curr = None, root

        if not root:
            return result

        stack.append(root)
        while len(stack) > 0:
            curr = stack[-1]
            if not prev or prev.left == curr or prev.right == curr:  # traverse down the tree
                if curr.left:
                    stack.append(curr.left)
                elif curr.right:
                    stack.append(curr.right)
            elif curr.left == prev:  # traverse up the tree from the left
                if curr.right:
                    stack.append(curr.right)
            else:  # traverse up the tree from the right
                result.append(curr.val)
                stack.pop()
            prev = curr

        return result

```

#### 练习

[http://www.lintcode.com/problem/binary-tree-postorder-traversal/](http://www.lintcode.com/problem/binary-tree-postorder-traversal/)





