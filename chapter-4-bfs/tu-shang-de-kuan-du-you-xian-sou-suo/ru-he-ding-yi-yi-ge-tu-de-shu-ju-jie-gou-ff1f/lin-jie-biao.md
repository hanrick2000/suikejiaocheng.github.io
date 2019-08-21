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

#### 使用 Map 和 Set（面试时）

也可以使用 HashMap 和 HashSet 搭配的方式来存储邻接表

Python:

```py
# 假设nodes为节点标签的列表:

# 使用了Python中的dictionary comprehension语法
adjacency_list = {x:set() for x in nodes}

# 另一种写法
adjacency_list = {}
for x in nodes:
    adjacency_list[x] = set()
```

其中 T 代表节点类型。通常可能是整数\(Integer\)。

  


这种方式虽然没有上面的方式更加直观和容易理解，但是在面试中比较节约代码量。

  


而自定义的方法，更加工程化，所以在面试中如果时间不紧张题目不难的情况下，推荐使用自定义邻接表的方式。

