# 90. 子集 II (Subsets II) · 2026-04-20

## 元信息
- 难度：Medium
- 所属模式：回溯算法 (Backtracking)
- 来源：LeetCode #90
- 语言：JavaScript

## Timebox
- 分配时长：30 分钟
- 实际用时：15 分钟
- 是否需要 LLM 提示：否 (由 AI 引导思路，代码独立完成剪枝逻辑)

## 核心不变量
"**树层去重**：在同一层决策中，相同的元素只允许作为起始点出现一次。通过 `i > start` 判定当前是否在处理同层后续备选方案，结合排序后的 `nums[i] == nums[i-1]` 实现精准剪枝。"

## 攻击向量
1. **排序先行**：必须通过 `sort` 让重复元素相邻，这是剪枝的前提。
2. **同层剪枝**：`if (i > start && nums[i] == nums[i-1]) continue;`。

## 模式 + 为什么这个模式适用
回溯算法（带剪枝）。处理含有重复元素的搜索问题时，通过剪掉决策树上的冗余分支，将解空间从“含重复”压缩为“唯一”。

## 最小骨架（回溯去重版）
```javascript
nums.sort((a, b) => a - b);
function backtrack(start, path) {
    res.push([...path]);
    for (let i = start; i < nums.length; i++) {
        // 同层去重
        if (i > start && nums[i] === nums[i-1]) continue;
        
        path.push(nums[i]);
        backtrack(i + 1, path);
        path.pop();
    }
}
```

## 触发信号
- "包含重复元素"
- "解集不能包含重复的子集/组合"
- "所有可能的解"

## 关键失误
- **忘记排序**：剪枝逻辑 `nums[i] == nums[i-1]` 依赖于数组有序。
- **混淆去重条件**：误写成 `i > 0` 会导致在递归深度方向也把重复元素删掉（比如无法生成 `[2, 2]`）。

## 下一题建议
39. 组合总和 (挑战：元素可重复使用，且无重复结果，考察对 `i` 和 `i + 1` 的控制)
