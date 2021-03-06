## 双向宽度优先搜索算法

双向宽度优先搜索 \(Bidirectional BFS\) 算法适用于如下的场景：

1. 无向图
2. 所有边的长度都为 1 或者长度都一样
3. 同时给出了起点和终点

以上 3 个条件都满足的时候，可以使用双向宽度优先搜索来求出起点和终点的最短距离。

### 算法描述

双向宽度优先搜索本质上还是BFS，只不过变成了起点向终点和终点向起点同时进行扩展，直至两个方向上出现同一个子节点，搜索结束。我们还是可以利用队列来实现：一个队列保存从起点开始搜索的状态，另一个保存从终点开始的状态，两边如果相交了，那么搜索结束。起点到终点的最短距离即为起点到相交节点的距离与终点到相交节点的距离之和。

**Q.双向BFS是否真的能提高效率？**  
假设单向BFS需要搜索 N 层才能到达终点，每层的判断量为 X，那么总的运算量为$$X ^ N$$  . 如果换成是双向BFS，前后各自需要搜索 N / 2 层，总运算量为$$2 * X ^ {N / 2}$$。如果 N 比较大且X 不为 1，则运算量相较于单向BFS可以大大减少，差不多可以减少到原来规模的根号的量级。

### 参考代码

Python:

```py
from collections import deque

def doubleBFS(start, end):
    if start == end:
        return 1

    # 分别从起点和终点开始的两个BFS队列
    startQueue, endQueue = deque(), deque()
    startQueue.append(start)
    endQueue.append(end)
    step = 0

    # 从起点开始和从终点开始分别访问过的节点集合
    startVisited, endVisited = set(), set()
    startVisited.add(start)
    endVisited.add(end)
    while len(startQueue) and len(endQueue):
        startSize, endSize = len(startQueue), len(endQueue)
        #　按层遍历
        step += 1
        for _ in range(startSize):
            cur = startQueue.popleft()
            for neighbor in cur.neighbors:
                if neighbor in startVisited: # 重复节点
                    continue
                elif neighbor in endVisited: # 相交
                    return step
                else:
                    startVisited.add(neighbor)
                    startQueue.append(neighbor)
        step += 1
        for _ in range(endSize):
            cur = endQueue.popleft()
            for neighbor in cur.neighbors:
                if neighbor in endVisited:
                    continue
                elif neighbor in startVisited:
                    return step
                else:
                    endVisited.add(neighbor)
                    endQueue.append(neighbor)

    return -1
```

### 学习建议

Bidirectional BFS 掌握起来并不是很难，算法实现上稍微复杂了一点（代码量相对单向 BFS 翻倍），掌握这个算法一方面加深对普通 BFS 的熟练程度，另外一方面，基本上写一次就能记住，如果在面试中被问到了如何优化 BFS 的问题，Bidirectional BFS 几乎就是标准答案了。

### 参考资料

[https://www.geeksforgeeks.org/bidirectional-search](https://www.geeksforgeeks.org/bidirectional-search)

### 应用例题

[Shortest Path in Undirected Graph](http://www.lintcode.com/zh-cn/problem/shortest-path-in-undirected-graph/)  
[Knight Shortest Path](http://www.lintcode.com/zh-cn/problem/knight-shortest-path/)  
[Knight Shortest Path II](http://www.lintcode.com/en/problem/knight-shortest-path-ii/)

