## BST 的增删查改

## 什么是二叉搜索树\(Binary Search Tree\)

**二叉搜索树**可以是一棵空树或者是一棵满足下列条件的[二叉树](https://zh.wikipedia.org/wiki/二叉树):

* 如果它的左子树不空，则左子树上所有节点值`均小于`它的根节点值。
* 如果它的右子树不空，则右子树上所有节点值`均大于`它的根节点值。
* 它的左右子树均为二叉搜索树\(BST\)。
* 严格定义下BST中是没有值相等的节点的\(No duplicate nodes\)。
  根据上述特性，我们可以得到一个结论：BST**中序遍历**得到的序列是**升序**的。如下述BST的中序序列为：\[1,3,4,6,7,8,10,13,14\]

![](http://media.jiuzhang.com/markdown/images/3/14/64328624-2749-11e8-b863-0242ac110002.jpg "BST")

### BST基本操作——增删改查\(CRUD\)

对于树节点的定义如下：

Python:

```py
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
```

#### 基本操作之查找\(Retrieve\)

* 思路

  * 查找值为**val**的节点，如果val小于根节点则在左子树中查找，反之在右子树中查找

* 代码实现

Python:

```py
def searchBST(root, val):
    if not root:
        return None # 未找到值为val的节点
    if val < root.val:
        return searchBST(root.left, val) # val小于根节点值，在左子树中查找哦
    elif val > root.val:
        return searchBST(root.right, val) # val大于根节点值，在右子树中查找
    else:
        return root
```

* 实战
  * [http://www.lintcode.com/en/problem/search-range-in-binary-search-tree/](http://www.lintcode.com/en/problem/search-range-in-binary-search-tree/)
  * [http://www.lintcode.com/en/problem/two-sum-bst-edtion/](http://www.lintcode.com/en/problem/two-sum-bst-edtion/)
  * [http://www.lintcode.com/en/problem/closest-binary-search-tree-value/](http://www.lintcode.com/en/problem/closest-binary-search-tree-value/)
  * [http://www.lintcode.com/en/problem/closest-binary-search-tree-value-ii/](http://www.lintcode.com/en/problem/closest-binary-search-tree-value-ii/)
  * [http://www.lintcode.com/en/problem/trim-binary-search-tree/](http://www.lintcode.com/en/problem/trim-binary-search-tree/)
  * [http://www.lintcode.com/en/problem/bst-swapped-nodes/](http://www.lintcode.com/en/problem/bst-swapped-nodes/)

#### 基本操作之修改\(Update\)

* 思路

  * 修改仅仅需要在查找到需要修改的节点之后，更新这个节点的值就可以了

* 代码实现

Python:

```py

```

* 实战
  * [http://www.lintcode.com/en/problem/bst-swapped-nodes/](http://www.lintcode.com/en/problem/bst-swapped-nodes/)

#### 基本操作之增加\(Create\)

* 思路

  * 根节点为空，则待添加的节点为根节点
  * 如果待添加的节点值小于根节点，则在左子树中添加
  * 如果待添加的节点值大于根节点，则在右子树中添加
  * 我们统一在树的叶子节点\(Leaf Node\)后添加

* 代码实现

Python:

```
def
insertNode
(root, node)
:
if
not
 root:

return
 node

if
 root.val 
>
 node.val:
        root.left = insertNode(root.left, node)

else
:
        root.right = insertNode(root.right, node)

return
 root
```

* 实战
  * [http://www.lintcode.com/en/problem/insert-node-in-a-binary-search-tree/](http://www.lintcode.com/en/problem/insert-node-in-a-binary-search-tree/)

#### 基本操作之删除\(Delete\)

* 思路\(最为复杂\)

  * 考虑待删除的节点为叶子节点，可以直接删除并修改父亲节点\(Parent Node\)的指针，需要区分待删节点是否为根节点
  * 考虑待删除的节点为单支节点\(只有一棵子树——左子树 or 右子树\)，与删除链表节点操作类似，同样的需要区分待删节点是否为根节点
  * 考虑待删节点有两棵子树，可以将待删节点与左子树中的最大节点进行交换，由于左子树中的最大节点一定为叶子节点，所以这时再删除待删的节点可以参考第一条
  * 详细的解释可以看
    [http://www.algolist.net/Data\_structures/Binary\_search\_tree/Removal](http://www.algolist.net/Data_structures/Binary_search_tree/Removal)

* 代码实现

Python:

```
def
removeNode
(root, value)
:

    dummy = TreeNode(
0
)
    dummy.left = root
    parent = findNode(dummy, root, value)
    node = 
None
if
 parent.left 
and
 parent.left.val == value:
        node = parent.left

elif
 parent.right 
and
 parent.right.val == value:
        node = parent.right

else
:

return
 dummy.left
    deleteNode(parent, node)

return
 dummy.left


def
findNode
(parent, node, value)
:
if
not
 node:

return
 parent

if
 node.val == value:

return
 parent

if
 value 
<
 node.val:

return
 findNode(node,node.left, value)

else
:

return
 findNode(node, node.right, value)


def
deleteNode
(parent, node)
:
if
not
 node.right:

if
 parent.left == node:
            parent.left = node.left

else
:
            parent.right = node.left

else
:
        temp = node.right
        father = node

while
 temp.left:
            father = temp
            temp = temp.left

if
 father.left == temp:
            father.left = temp.right

else
:
            father.right = temp.right

if
 parent.left == node:
            parent.left = temp

else
:
            parent.right = temp
        temp.left = node.left
        temp.right = node.right
```

* 实战
  * [http://www.lintcode.com/en/problem/remove-node-in-binary-search-tree/](http://www.lintcode.com/en/problem/remove-node-in-binary-search-tree/)
  * [http://www.lintcode.com/en/problem/trim-binary-search-tree/](http://www.lintcode.com/en/problem/trim-binary-search-tree/) 



