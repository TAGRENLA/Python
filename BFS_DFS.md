图的遍历需要通过搜索方法来实现遍历操作。图的遍历可以分为两种：

- `广度`优先遍历[breadth‑first-traversal]
- `深度`优先遍历[depth‑first-traversal]

通常分别称其为`BFS`、`DFS`

# BFS:kissing_heart:

广度优先搜索算法是一种由近及远的方式，从某个节点出发，始终优先访问距离最近的顶点，并一层层向外扩张。如下图所示：



![](https://tagrenla.oss-cn-beijing.aliyuncs.com/%E6%97%A0%E6%A0%87%E9%A2%98%E5%8E%9F%E5%9E%8B%E5%9B%BE(1)%20(1).png)



## 算法实现

BFS通常借助队列实现，利用队列先进先出的性质，

1. 将起始节点添加到队列中，并开启循环。
2. 每次循环将将`队首弹出`队列，并将与其连接的节点添加到队列的`尾`部。
3. 循环步骤`2`，直到队列中的所有的节点都被访问完成后结束！

为了防止重复遍历顶点，我们需要借助一个哈希表` visited` 来记录哪些节点已被访问。

```python
def bfs(graph, start_vertex):
    visited = set()                 # 定义集合 存储 已经遍历过的节点
    queue = [start_vertex]          # 使用队列先进先出的性质，进行遍历，初始将头节点添加到队列中
    while queue:                    # 当这个队列中有元素的时候   进入循环
        vertex = queue.pop(0)       # 弹出列表的第一个节点 
        if vertex not in visited:   # 如果这个节点没有被遍历过
            print(vertex, end=' ')  # 访问节点，可以进行相关操作
            visited.add(vertex)     # 访问结束后==>将其添加到已经遍历的集合中
            if vertex in graph:     # 如果这个节点还有与之相连的节点，将这些节点添加到队列的尾部
                queue.extend(neighbor for neighbor in graph[vertex] if neighbor not in visited)

graph = {
    0:[1,3],
    1:[0,2,4],
    3:[0,4,6],
    2:[1,5],
    4:[1,5,7,3],
    5:[8,4,2],
    6:[3,7],
    7:[6,4,8],
    8:[7,5],
}

print("BFS遍历结果：")
bfs(graph, 0)
```

## 详细的图解

![](https://tagrenla.oss-cn-beijing.aliyuncs.com/%E6%97%A0%E6%A0%87%E9%A2%98%E5%8E%9F%E5%9E%8B%E5%9B%BE(7)%20(2).png)

> 综上所述，`BFS`的精髓就是：
>
> - 将队首元素取出，添加到res(遍历结果)中，并添加到visited中
> - 将与该队首节点相邻的节点添加到队尾中
> - 重复遍历队列中的节点，直到队列为空，BFS结束



:sunglasses:**BFS（广度优先搜索）的关键点是`维护一个队列`，从起始节点开始，`逐层将节点加入队列`，然后按照队列中的顺序依次探索各层的节点，直到找到目标或者队列为空。**



## 遍历序列是否唯一？

不唯一。广度优先遍历只要求“由近及远”的顺序遍历，而`多个相同距离的节点的遍历顺序是允许被打乱的`。

---

# DFS:tired_face:

`深度优先遍历是一种优先一条路走到底，无路可走时再回头的遍历方式`，如下图所示：

![](https://tagrenla.oss-cn-beijing.aliyuncs.com/%E6%97%A0%E6%A0%87%E9%A2%98%E5%8E%9F%E5%9E%8B%E5%9B%BE(8)%20(1).png)

## 算法实现

**DFS的基本步骤**：

1. 选择一个起始节点（通常是根节点），将其标记为已访问（创建一个哈希表）。
2. 探索当前节点的邻居节点，这些邻居节点是从当前节点直接可达的节点中尚未被访问的节点。
3. 递归地应用DFS算法到其中一个邻居节点，即深入到一个尚未探索的分支。这会一直持续下去，直到达到一个没有未访问邻居的节点。
4. 当到达一个没有未访问邻居的节点时，回溯到上一个节点，检查是否还有其他未探索的分支。
5. 重复步骤3和步骤4，直到所有节点都被访问为止。

代码如下：

~~~python
visited = set()                               # 因为要涉及递归  所以一定要定义为全局变量
def dfs(graph, vertex, visited):
    if vertex not in visited:                 # 如果节点未被访问
        print(vertex,end=' ')                 # 访问该节点==可以进行相关的操作
        visited.add(vertex)                   #  将访问的节点  添加到  已经访问的  集合中
        if vertex in graph:                   # 如果还存在与之相连的节点 
            for neighbor in graph[vertex]:    # 将与之相连的节点进行相同的操作
                dfs(graph, neighbor, visited) # 深度优先

graph = {
    0:[1,3],
    1:[0,2,4],
    3:[0,4,6],
    2:[1,5],
    4:[1,5,7,3],
    5:[8,4,2],
    6:[3,7],
    7:[6,4,8],
    8:[7,5],
}
 

print("DFS遍历结果：")
dfs(graph, 0, visited)
~~~

## 详细图解

![](https://tagrenla.oss-cn-beijing.aliyuncs.com/%E6%97%A0%E6%A0%87%E9%A2%98%E5%8E%9F%E5%9E%8B%E5%9B%BE(9)%20(1).png)

> ***DFS精髓***：
>
> DFS（深度优先搜索）的核心思想是使用`递归`来深入探索图或树的深度，直到无法继续为止，然后`回溯`到上一层。

## 遍历序列是否唯一？

与广度优先遍历类似，深度优先遍历序列的顺序也不是唯一的。给定某顶点，先往那个方向探索都可以，即进阶顶点的顺序是可以任意打乱，都是深度优先遍历





