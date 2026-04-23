# 动态规划 (Dynamic Programming)

动态规划的核心在于：**通过组合子问题的解来解决原问题，并利用空间换时间，避免重复计算**。

## 核心三要素

1.  **状态定义**：`dp[i]` 到底代表什么？（如：爬到第 $i$ 级的方法数）。
2.  **状态转移方程**：`dp[i]` 如何从之前的状态推导出来？（如：`dp[i] = dp[i-1] + dp[i-2]`）。
3.  **边界条件**：最基础的已知项是什么？（如：`dp[1] = 1, dp[2] = 2`）。

## 核心不变量
- **记住过去，推导未来**：每个状态只计算一次并存入备忘录。

## 触发信号
- 求最值、求方案数。
- 具有重叠子问题（如递归过程中多次算同一个值）。
- 具有最优子结构（大问题的最优解包含小问题的最优解）。

## 最小骨架 (Java/JS)
```javascript
function solve(n) {
  if (n <= base) return initialValue;
  let dp = new Array(n + 1);
  dp[0] = base0;
  dp[1] = base1;
  for (let i = 2; i <= n; i++) {
    dp[i] = transferFunction(dp[i-1], dp[i-2], ...);
  }
  return dp[n];
}
```

## 训练记录
- [70. 爬楼梯](../training-logs/70-climbing-stairs.md) (2026-04-22)
- [509. 斐波那契数](../training-logs/509-fibonacci-number.md) (2026-04-22)
