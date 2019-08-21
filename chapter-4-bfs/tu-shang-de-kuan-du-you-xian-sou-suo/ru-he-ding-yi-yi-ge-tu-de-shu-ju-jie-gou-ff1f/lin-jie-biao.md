## 邻接表

邻接表 \(Adjacency List\)

```
[
  [1],
  [0,2,3],
  [1],
  [1]
]

```

这个图表示 0 和 1 之间有连边，1 和 2 之间有连边，1 和 3 之间有连边。即每个点上存储自己有哪些邻居（有哪些连通的点）。  
这种方式下，空间耗费和边数成正比，可以记做 O\(m\)，m代表边数。m最坏情况下虽然也是 O\(n^2\)，但是邻接表的存储方式大部分情况下会比邻接矩阵更省空间。

#### 自定义邻接表

可以用自定义的类来实现邻接表

Python:

```py
def DirectedGraphNode:
    def __init__(self, label):
        self.label = label
        self.neighbors = []  # a list of DirectedGraphNode's
		...
```

其中 neighbors 表示和该点连通的点有哪些。





