# 图遍历 (Graph Traversal)

图遍历的核心在于：**不重复、不遗漏地访问所有连通的节点**。

## 核心算法

### 1. DFS (深度优先搜索)
- **核心思想**：一条路走到黑，撞墙再回头。
- **实现方式**：通常使用**递归**。
- **适用场景**：路径搜索、连通块统计、拓扑排序。

### 2. BFS (广度优先搜索)
- **核心思想**：地毯式搜索，层层向外扩散。
- **实现方式**：通常使用**队列 (Queue)**。
- **适用场景**：最短路径问题（非负权）。

## 核心不变量
- **状态标记**：必须记录已访问的节点（如 `visited` 数组），防止死循环。
- **边界检查**：在网格图中，必须检查坐标是否越界。

## 最小骨架 (DFS)
```javascript
function dfs(grid, r, c, visited) {
  if (isInvalid(r, c) || isVisited(r, c) || isWater(r, c)) return;
  markVisited(r, c);
  dfs(grid, r - 1, c, visited); // 上
  dfs(grid, r + 1, c, visited); // 下
  dfs(grid, r, c - 1, visited); // 左
  dfs(grid, r, c + 1, visited); // 右
}
```

## 训练记录
- [200. 岛屿数量](../training-logs/200-number-of-islands.md) (2026-04-22)
