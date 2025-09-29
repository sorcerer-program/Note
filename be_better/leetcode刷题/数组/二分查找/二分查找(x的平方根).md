---
date: 2024-07-22
tags:
  - 二分查找
  - 数组
  - 算法
  - leetcode69
---

# 二分查找(x的平方根)

## 题目

![[leetcode69.png]]

## 理解关键点

> 当  `middle *  middle <= x`  的时候说明middle是潜在的答案，但是答案可能更大，我们要继续往右找，所以先记录  `ans = middle`  ，再将 left 刷新。

> 为了防止溢出，将  `middle *  middle <= x`  改为 `middle <=  x / middle`  

> 这里采用的是左闭右闭，这里注意的是原本  `right = x - 1`   改成了 `right == x`  (左闭右开同理)
> 区分基础二分法，因为基础中是基于数组的，最末下标是  `numsSize - 1`  ，本题不存在下标越界，最末就是 x ，左闭右开，`right == x + 1` ，左闭右闭，`right = x` 

## 解答

```c
int mySqrt(int x) {
    if (x == 0) return 0;

    int left = 1, right = x, ans = 0;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (mid <= x / mid) {
            ans = mid;
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return ans;
}
```

对比分析[[二分查找(基础)]]