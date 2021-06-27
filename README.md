# Daily leetcode

## Leetcode 思路总结

### 动态规划问题：

1、例：从  `[1,1,1,1,1,2,2]`  中挑选元素，计算出所有相加等于 2 的组合数。

假定 `dp[i] = x` 表示相加等于 `i` 的方案数为 `x` 。

则可以确定的初始值为 `dp[0] = 1`，即相加等于 0 的方案数只有一种，就是一个元素都不选。

分个选上列表中的元素 `num` ，重新计算 `dp[num - 1]` 至 `dp[i]` 的值（`num > i` 则不会改別任何方案数，大于 `num - 1`，即大于等于 `num` 的方案数都有可能改变，题目中 `i = 2`）

每当多选一个 `num` 时，不难发现动态方程为 `dp[i] = dp[i]`(当前已知相加等于 i 的方案数) + `dp[i - num]`(选上这个元素 `num` 多出来的方案数，就是 `dp[i - num]` 的方案数，因为 **i - num + num = i** )

即：`dp[ i ] = dp[ i ] + dp[ i-num ]`

下面列举详细：

 | 选取      |       0 |       1        |       2        |
 | :-------- | ------: | :------------: | :------------: |
 | num  =  1 | 1(已知) | 1 **（后算）** | 0 **（先算）** |
 | num  =  1 |       1 |       2        |       1        |
 | num  =  1 |       1 |       3        |       3        |
 | num  =  1 |       1 |       4        |       6        |
 | num  =  1 |       1 |       5        |       10       |
 | num  =  2 |       1 |       5        |       11       |
 | num  =  2 |       1 |       5        |       12       |

所以最后得出，从  `[1,1,1,1,1,2,2]`  中挑选元素，相加等于 2 的组合数为 `dp[2] = 12` 种

**第一列解释：**

刚开始只有 `dp[0] = 1` 是已知的，`dp[1]` 和 `dp[2]` 都是 0，计算 `dp[2] = dp [2]  + dp[2-1(num)] = dp[2] + dp[1] = 0 + 0 = 0` （原来相加等于 1 的方案加上这个 1 都等于 2，即选上这个 1 后，多出来这么多相加等于 2 的方案）

**倒序遍历**：这里要先算 `dp[2]`，因为如果先算 `dp[1]` ，那么计算 `dp[2]` 的时候，`dp[1]` 已经不是开始时候的 `dp[1]` 了，已经不为 0 了，而第一次 `dp[1]` 应该为 0。

## 搜索问题：

# 深度优先（DFS Depth-First-Search）

深度优先用递归的形式，用到了栈结构，先进后出

利用深度优先搜索算法可以产生目标图的相应拓扑排序表，利用拓扑排序表可以方便的解决很多相关的图论问题，如最大路径问题，一般是解决连通性问题

# 广度优先（BFS Breadth-First-Search）

广度优先用队列的形式，先进先出

BFS 一般是解决最短路径问题，Dijkstra 和 Astar 算法都属于广度优先，前者是后者的特殊形式（评估函数为 0）