# 二分查找 / Binary Search

## 一句话定义
在具有单调性的搜索空间中，通过不断比较中点与目标值，每次将搜索范围缩小一半。

## 核心不变量
- **左闭右闭 `[left, right]`**：`left = 0, right = n-1, while (left <= right)`，`mid` 排除法更新 `left = mid + 1` 或 `right = mid - 1`。
- **左闭右开 `[left, right)`**：`left = 0, right = n, while (left < right)`，`mid` 更新 `left = mid + 1` 或 `right = mid`。

## 触发信号（气味清单）
题目里出现以下任一线索，就应该立刻想到这个模式：
- 线索 1：数组有序（升序或降序）。
- 线索 2：要求在 $O(\log n)$ 时间复杂度内解决问题。
- 线索 3：寻找满足条件的第一个或最后一个位置（如：找到数组中 >= target 的第一个数）。
- 线索 4：在确定范围的整数内寻找最优解（如：吃香蕉的最快速度、运送货物的最小运载量）。

## 反触发信号（看起来像但其实不是）
- 例：数组无序且需要线性查找 → 除非先排序。
- 例：数据量很小且操作频繁 → 暴力法可能比排序+二分更直接。

## 最小骨架（查找数值版）
```javascript
let left = 0, right = nums.length - 1;
while (left <= right) {
    let mid = left + Math.floor((right - left) / 2);
    if (nums[mid] === target) return mid;
    else if (nums[mid] < target) left = mid + 1;
    else right = mid - 1;
}
return -1;
```

## 最小骨架（寻找左边界版 - 如果有重复数）
```javascript
let left = 0, right = nums.length - 1;
while (left <= right) {
    let mid = left + Math.floor((right - left) / 2);
    if (nums[mid] < target) left = mid + 1;
    else if (nums[mid] > target) right = mid - 1;
    else right = mid - 1; // 关键：等于 target 时继续向左压缩寻找第一个
}
if (left >= nums.length || nums[left] !== target) return -1;
return left;
```

## 常见变体
| 变体 | 关键差异 | 代表题 |
| :--- | :--- | :--- |
| 基础查找 | 找到直接返回 | 704. 二分查找 |
| 寻找边界 | 等于时不断收缩另一侧 | 34. 查找第一个/最后一个位置 |
| 旋转数组 | 结合分段有序讨论 | 33. 搜索旋转排序数组 |
| 二分答案 | 在可能的答案范围内折半搜索 | 875. 爱吃香蕉的珂珂 |

## 我做过的题（按时间倒序）
| 日期 | 题目 | 难度 | 角色 | Log |
| :--- | :--- | :--- | :--- | :--- |
| 2026-04-17 | 34. 查找第一个和最后一个位置 | Medium | 进阶 (寻找边界) | [log](../training-logs/2026-04-17-search-range.md) |
| 2026-04-17 | 704. 二分查找 | Easy | 首次引入 | [log](../training-logs/2026-04-17-binary-search.md) |

## 踩过的坑
- 计算 `mid` 时没注意大数溢出。
- 循环条件 `left <= right` 与更新逻辑 `left = mid + 1` 不匹配导致死循环。
- 返回值在查找边界场景中需要额外校验越界和值不匹配情况。
- 在寻找边界时，即使找到 `nums[mid] === target`，也要继续缩小范围。

## 下一道值得挑战的题
33. 搜索旋转排序数组 (掌握分段有序情况下的二分判断)


## 最近复述（Verbalization 版本）
就像在一堆已经排好队的书里找你要的那一本。先看最中间那本，如果它号大，你就只看左边那一半；号小就看右边那一半。直到两边的人都看完了或者你找到了为止。

## 状态
- 当前状态：`学习中`
- 最后一次实战：2026-04-17
- 下一次复习建议：2026-04-24
