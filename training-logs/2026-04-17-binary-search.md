# 704. 二分查找 · 2026-04-17

## 元信息
- 难度：Easy
- 所属模式：二分查找 (Binary Search)
- 来源：LeetCode #704
- 语言：JavaScript

## Timebox
- 分配时长：10 分钟
- 实际用时：5 分钟
- 是否需要 LLM 提示：否

## 核心不变量
"搜索区间 `[left, right]` 始终包含 target（如果存在）。每一步通过比较 `mid` 与 `target`，将搜索空间减半。"

## 攻击向量
标准左闭右闭区间 `[0, n-1]`，利用 `while (left <= right)` 进行迭代搜索。

## 模式 + 为什么这个模式适用
二分查找。由于数组已按升序排列（单调性），我们可以通过排除法在 $O(\log n)$ 时间内定位元素。

## 最小骨架（基础二分查找）
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

## 我的写法 vs 最优解（差异对照）
| 维度 | 我的写法 | 最优解 | 差异原因 |
| :--- | :--- | :--- | :--- |
| 时间复杂度 | O(log n) | O(log n) | 一致 |
| 空间复杂度 | O(1) | O(1) | 一致 |
| mid 计算 | `Math.floor((l+r)/2)` | `l + Math.floor((r-l)/2)` | 后者可防止大数相加溢出 |

## 触发信号
- 数组有序（或具有局部单调性）。
- 要求 $O(\log n)$ 复杂度。
- 在数值范围内寻找满足条件的极值。

## 关键失误
如果不更新 `left = mid + 1` 或 `right = mid - 1`，在只有两个元素且没找到目标时可能导致死循环。

## 口头讲解版本
就像在一本按字母排序的字典里查单词。先翻到中间那一页，如果中间的字比你要查的大，那就只在前半本里找；如果小，就只在后半本里找。每次都翻剩下的那一半，很快就能翻到那一页。

## 下一题建议
34. 在排序数组中查找元素的第一个和最后一个位置 (理解如何二分查找左右边界)
