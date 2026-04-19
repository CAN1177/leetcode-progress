# 102. 二叉树的层序遍历 · 2026-04-19

## 元信息
- 难度：Medium
- 所属模式：树的广度优先搜索 (Tree BFS)
- 来源：LeetCode #102
- 语言：JavaScript

## Timebox
- 分配时长：25 分钟
- 实际用时：10 分钟
- 是否需要 LLM 提示：否 (由 AI 引导思路，代码独立完成)

## 核心不变量
"在 `while` 循环内部处理每一层之前，通过 `levelSize = queue.length` 锁定当前层的边界。所有新入队的子节点都在此边界之后，保证层级不发生混淆。"

## 攻击向量
利用队列 (Queue) 先进先出的特性。每次从队列中弹出 `levelSize` 个节点，并将它们的值放入该层的结果数组，同时将它们的子节点入队。

## 模式 + 为什么这个模式适用
BFS (广度优先搜索)。本题要求“层序遍历”，即按照从上到下、从左到右的顺序逐层访问。BFS 天生适合处理层级关系和寻找最短路径。

## 最小骨架（BFS 层序遍历版）
```javascript
const queue = [root];
while (queue.length > 0) {
    const levelSize = queue.length;
    for (let i = 0; i < levelSize; i++) {
        const node = queue.shift();
        // 处理 node...
        if (node.left) queue.push(node.left);
        if (node.right) queue.push(node.right);
    }
}
```

## 我的写法 vs 最优解（差异对照）
| 维度 | 我的写法 | 最优解 | 差异原因 |
| :--- | :--- | :--- | :--- |
| 队列实现 | `Array.shift()` | 双指针模拟队列 / Deque | `Array.shift()` 在 JS 中是 $O(n)$，在大规模数据下性能受限 |
| 逻辑正确性 | 完全一致 | 完全一致 | 核心在于锁定 `levelSize` |

## 触发信号
- "二叉树的层序/逐层遍历"
- "从左到右访问每一层"
- "树/图的最短路径"

## 关键失误
- 忘记判空 `if (!root) return []`。
- 直接在 `for` 循环中使用 `queue.length` 而不是固定的 `levelSize`。

## 下一题建议
103. 二叉树的锯齿形层序遍历 (BFS 变体：考察对层内处理顺序的灵活切换)
