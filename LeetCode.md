## 1.BFS

### [994. 腐烂的橘子](https://leetcode.cn/problems/rotting-oranges/)

在给定的 m x n 网格 grid 中，每个单元格可以有以下三个值之一：

值 0 代表空单元格；
值 1 代表新鲜橘子；
值 2 代表腐烂的橘子。
每分钟，腐烂的橘子 周围 4 个方向上相邻 的新鲜橘子都会腐烂。

返回 直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。如果不可能，返回 -1 。

  **示例 1：** ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/16/oranges.png) 

```
输入：grid = [[2,1,1],[1,1,0],[0,1,1]]
输出：4
```

 **示例 2：** 

```
输入：grid = [[2,1,1],[0,1,1],[1,0,1]]
输出：-1
解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个正向上。
```

 **示例 3：** 

```
输入：grid = [[0,2]]
输出：0
解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。
```

**提示：**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j]` 仅为 `0`、`1` 或 `2`

```python
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        row = len(grid)
        col = len(grid[0])
        # 广度优先遍历BFS，需要用队列来存储需要被遍历的节点，对本题来说，即值为2的节点都需要被遍历。
        queue = []
        time = 0
        dir = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 2:
                    queue.append((i, j, time))
        while queue:
            i, j, time = queue.pop(0)
            for di, dj in dir:
                if 0 <= i + di < row and 0 <= j + dj < col and grid[i + di][j + dj] == 1:
                    grid[i + di][j + dj] = 2
                    queue.append((i + di, j + dj, time + 1))
        for g in grid:
            if 1 in g:
                return -1
        return time
"""
BFS和DFS区别：
广度优先搜索算法（Breadth-First-Search，缩写为 BFS），是一种利用队列实现的搜索算法。简单来说，其搜索过程和 “湖面丢进一块石头激起层层涟漪” 类似。用于解决最短路径问题。
深度优先搜索算法（Depth-First-Search，缩写为 DFS），是一种利用递归实现的搜索算法。简单来说，其搜索过程和 “不撞南墙不回头” 类似。
https://cuijiahua.com/blog/2018/01/alogrithm_10.html
https://leetcode-cn.com/problems/rotting-oranges/solution/li-qing-si-lu-wei-shi-yao-yong-bfsyi-ji-ru-he-xie-/
"""
"""
与DFS几道题对比：
该题初始状态可能同时存在多个腐烂的橘子，接下来会同时开始腐烂，不能像DFS那几道题一样，随便找到一个腐烂的句子就开始无脑”暴力搜索“。
https://blog.csdn.net/qq_43857314/article/details/88077221
"""
"""
心得：（1）BFS用队列存储需要被遍历的节点
     （2）DFS实际上就是递归
"""
```

## 2.差分

### [370. 区间加法](https://leetcode.cn/problems/range-addition/)

假设你有一个长度为 n 的数组，初始情况下所有的数字均为 0，你将会被给出 k 个更新的操作。

其中，每个操作会被表示为一个三元组：[startIndex, endIndex, inc]，你需要将子数组 A[startIndex ... endIndex]（包括 startIndex 和 endIndex）增加 inc。

请你返回 k 次操作后的数组。

 **示例:** 

```
输入: length = 5, updates = [[1,3,2],[2,4,3],[0,2,-2]]
输出: [-2,0,3,5,3]
```

 **解释:** 

```
初始状态:
[0,0,0,0,0]

进行了操作 [1,3,2] 后的状态:
[0,2,2,2,0]

进行了操作 [2,4,3] 后的状态:
[0,2,5,5,3]

进行了操作 [0,2,-2] 后的状态:
[-2,0,3,5,3]
```

```python
class Solution:
    def getModifiedArray(self, length: int, updates: List[List[int]]) -> List[int]:
        diff = [0] * length
        for t in range(len(updates)):
            i, j, tmp = updates[t]
            diff[i] += tmp
            if j + 1 < length:
                diff[j + 1] -= tmp
        for i in range(1, len(diff)):
            diff[i] = diff[i] + diff[i - 1]
        return diff
```

#### [1094. 拼车](https://leetcode.cn/problems/car-pooling/)

车上最初有 capacity 个空座位。车 只能 向一个方向行驶（也就是说，不允许掉头或改变方向）

给定整数 capacity 和一个数组 trips ,  trip[i] = [numPassengersi, fromi, toi] 表示第 i 次旅行有 numPassengersi 乘客，接他们和放他们的位置分别是 fromi 和 toi 。这些位置是从汽车的初始位置向东的公里数。

当且仅当你可以在所有给定的行程中接送所有乘客时，返回 true，否则请返回 false。

 **示例 1：** 

```
输入：trips = [[2,1,5],[3,3,7]], capacity = 4
输出：false
```

 **示例 2：** 

```
输入：trips = [[2,1,5],[3,3,7]], capacity = 5
输出：true
```

```python
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        diff = [0] * 1001
        for t in range(len(trips)):
            tmp, i, j = trips[t]
            diff[i] += tmp
            # 先下后上，因此本题是 diff[j] -= tmp，而不是 diff[j+1] -= tmp
            if j < 1001:
                diff[j] -= tmp
        if diff[0] > capacity:
            return False
        # 遍历不包括查分数组的第一项，因此index = 0要单独考虑
        for i in range(1, 1001):
            diff[i] = diff[i] + diff[i - 1]
            if diff[i] > capacity:
                return False
        return True
```

#### [1109. 航班预订统计](https://leetcode.cn/problems/corporate-flight-bookings/)

## 3.DFS

#### [200. 岛屿数量](https://leetcode.cn/problems/number-of-islands/)

#### [695. 岛屿的最大面积](https://leetcode.cn/problems/max-area-of-island/)

#### [1219. 黄金矿工](https://leetcode.cn/problems/path-with-maximum-gold/)

## 4.动态规划

#### [198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

#### [416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/)

#### [1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii/)



