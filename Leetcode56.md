---
title: Leetcode 56. Merge Intervals 合并区间
author: Mark
summary: 升序排列数组，遍历区间，若大于等于左端点，则于遍历区间的右端点进行对比，确立右端点界限，若小于左端点，则确立遍历节点为当前节点
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: 2ac753c1
date: 2021-09-27 19:49:00
---

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

 

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

 

**Constraints:**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`





## 分析

1.合并区间首先要确立左边界，应当对intervals数组以每个区间的左端点进行升序排序

2.然后将当前区间加入list之中，在list中与后续遍历区间的左端点进行对比

+ 若大于等于左端点，则于遍历区间的右端点进行对比，确立右端点界限
+ 若小于左端点，则确立遍历节点为当前节点

3.将list转换为数组，采用`ans.toArray(new int[ans.size()][])`的方式

#### 方法

初始化list存储结果区间，遍历区间，采取以上思想，返回不重叠区间数组

#### 代码

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> ans=new ArrayList();
        if(intervals.length<=1) {
            return intervals;
        }
        Arrays.sort(intervals,(i1,i2)->i1[0]-i2[0]);
        int[] cur=intervals[0];
        ans.add(cur);
        for(int[] interval:intervals) {
            if(cur[1]>=interval[0]) {
                cur[1]=Math.max(cur[1],interval[1]);
            } else {
                cur=interval;
                ans.add(cur);
            }
        }
        return ans.toArray(new int[ans.size()][]);
    }
}
```

