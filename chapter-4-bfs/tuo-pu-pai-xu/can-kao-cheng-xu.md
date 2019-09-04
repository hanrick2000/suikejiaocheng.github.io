## 参考程序

#### 提交地址

这是 LintCode 上的题目：[Topological Sorting](http://www.lintcode.com/problem/topological-sorting/)

参考程序

```java
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */    
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // map 用来存储所有节点的入度，这里主要统计各个点的入度
        HashMap<DirectedGraphNode, Integer> map = new HashMap();
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (map.containsKey(neighbor)) {
                    map.put(neighbor, map.get(neighbor) + 1);
                } else {
                    map.put(neighbor, 1); 
                }
            }
        }

        // 初始化拓扑序列为空
        ArrayList<DirectedGraphNode> result = new ArrayList<DirectedGraphNode>();

        // 把所有入度为0的点，放到BFS专用的队列中
        Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
        for (DirectedGraphNode node : graph) {
            if (!map.containsKey(node)) {
                q.offer(node);
                result.add(node);
            }
        }

        // 每次从队列中拿出一个点放到拓扑序列里，并将该点指向的所有点的入度减1
        while (!q.isEmpty()) {
            DirectedGraphNode node = q.poll();
            for (DirectedGraphNode n : node.neighbors) {
                map.put(n, map.get(n) - 1);
                // 减去1之后入度变为0的点，也放入队列
                if (map.get(n) == 0) {
                    result.add(n);
                    q.offer(n);
                }
            }
        }

        return result;
    }
}
```

```py
#BFS
"""
Definition for a Directed graph node
class DirectedGraphNode:
    def __init__(self, x):
        self.label = x
        self.neighbors = []
"""

class Solution:
    """
    @param graph: A list of Directed graph node
    @return: Any topological order for the given graph.
    """
    def topSort(self, graph):
        node_to_indegree = self.get_indegree(graph)

        # bfs
        order = []
        start_nodes = [n for n in graph if node_to_indegree[n] == 0]
        queue = collections.deque(start_nodes)
        while queue:
            node = queue.popleft()
            order.append(node)
            for neighbor in node.neighbors:
                node_to_indegree[neighbor] -= 1
                if node_to_indegree[neighbor] == 0:
                    queue.append(neighbor)

        return order

    def get_indegree(self, graph):
        node_to_indegree = {x: 0 for x in graph}

        for node in graph:
            for neighbor in node.neighbors:
                node_to_indegree[neighbor] += 1

        return node_to_indegree
```

```py
#DFS (不推荐面试使用)
"""
Definition for a Directed graph node
class DirectedGraphNode:
    def __init__(self, x):
        self.label = x
        self.neighbors = []
"""

class Solution:
    """
    @param graph: A list of Directed graph node
    @return: Any topological order for the given graph.
    """
    def topSort(self, graph):
        indegree = {}
        for x in graph:
            indegree[x] = 0

        for i in graph:
            for j in i.neighbors:
                indegree[j] += 1

        ans = []
        for i in graph:
            if indegree[i] == 0:
                self.dfs(i, indegree, ans)
        return ans

    def dfs(self, i, indegree, ans):
        ans.append(i)
        indegree[i] -= 1
        for j in i.neighbors:
            indegree[j] -= 1
            if indegree[j] == 0:
                self.dfs(j, indegree, ans)
```

其他语言的参考程序请见：

[http://www.jiuzhang.com/solutions/topological-sorting/](http://www.jiuzhang.com/solutions/topological-sorting/)

