## 练习：链表转平衡排序二叉树

题目描述

将有序链表转换为平衡的排序二叉树。

LintCode 练习地址：  
[http://www.lintcode.com/en/problem/convert-sorted-list-to-balanced-bst/](http://www.lintcode.com/en/problem/convert-sorted-list-to-balanced-bst/)

### 粗暴的算法

可以十分容易想到一个一个 $$O(nlogn)$$ 的分治算法，以链表作为参数，二叉树作为返回值：

Python:

```py
def convert(head):
    if not head:
        return null
				
    # find the following three nodes in the linked list
    # .... prev -> mid -> next ...
    # prev.next = null; // break the connect between prev & mid
		
		root = TreeNode(mid.val)
    root.left = convertListBBT(head)
    root.right = convertListBBT(next)
    return root

```

算法的大致思路就是，找到链表中点和他前后的点，然后左边的部分递归生成一棵左子树，右边的部分递归生成一棵右子树，再和中间的点拼接起来就好了。

这个算法我们不难发现他的时间复杂度是$$O(nlogn)$$的，因为找到中点的时间复杂度是$$O(n)$$，因此可以用 T 函数推算法来进行推算：

```
T(n) = 2 * T(n/2) + O(n) = O(nlogn)
```

### 优化的算法

为了优化这个算法，我们给分治函数带上了一个参数 n 代表目前打算去转换 head 开始，长度为 n 那么多个节点，让其变为 Balanced Binary Tree。递归函数接口如下：

Python

```py
"""
Returns a TreeNode.
"""
def convert(head, n):
```

这样，我们不用真正把链表从 prev 和 mid 之间断开。可以利用对第二个参数的大小控制来让处理规模缩小。

但是虽然我们可以很快的调用`convert(head, n / 2)`，让链表的一半变成二叉树。但是如何很快知道链表的中点呢？这里的办法是，如果我们把 head 放在参数里，那么就无法利用 convert 函数对 head 进行挪动了，所以我们把 head 挪出来，放到全局，作为一个全局变量。这样之后函数的接口改为：

Python:

```py
class Solution:
    def __init(self):
        self.current = None

    def convert(self, n):
        # ...

    def sortedListToBST(self, head):
        self.current = head
        self.convert(getLength(head));
```

这里我们在全局放了一个 current 指针，这个指针会指向当前还没有被变成 Tree 的下一个 List 上的节点。因此如果我们把左子树变成 Tree 以后，current 就要让他指向 List 上的下一个点，也就是中间的这个点了。

算法有一些绕，建议使用几个小数据模拟整个算法的执行过程。  
完整参考程序见：  
[http://www.jiuzhang.com/solution/convert-sorted-list-to-balanced-bst/](http://www.jiuzhang.com/solution/convert-sorted-list-to-balanced-bst/)

#### 完整算法描述如下：

1. 首先求得整个list的长度 O\(n\)
2. 利用 helper 函数进行递归，helper\(head, len\) 表示把从 head 开始的，长度为len的链表，转换为一个bst并且return。与此同时，把global variable的指针挪到head开始的第 len + 1个listnode上。

那么 convert\(head, len\) 就可以分为，三个步骤：

1. 把head开头的长度为 len/2的先变成bst，也就是我们的左子树，convert\(head, len / 2\)。这个时候他顺便会把global variable 挪到第len / 2 + 1的那个node，这个就是我们的root。
2. 然后得到了root之后，把global variable 往下挪一个挪到 第 len/2 + 2个点，也就是右子树开头的那个点，然后调用 convert\(global variable, len - len/2 -1\)，构造出右子树。
3. 然后把root，左子树，右子树，拼接在一起，return

这个题算法框架就是这样，如果不是很明白的话，建议模拟一个小数据，比如 5个节点的情况。模拟几个数据结合算法的思路来分析，就应该可以明白。这个题的这种解法背下来就好了。  




