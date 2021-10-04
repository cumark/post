---
title: Leetcode 410. Split Array Largest Sum 分割数组的最大值
author: Mark
summary: >-
  应对数组问题，可以考虑二分搜索，首先要确定上下界。由于各自和的最大值会在max（nums[i]）和sum之间，可以以max为左边界，sum为右边界，利用二分搜索不断接近并得到答案。
tags:
  - leetcode
  - algorithm
  - binarySearch
categories:
  - 算法
abbrlink: af957438
date: 2021-09-28 13:15:00
---

Given an array `nums` which consists of non-negative integers and an integer `m`, you can split the array into `m` non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these `m` subarrays.

 

**Example 1:**

```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

**Example 2:**

```
Input: nums = [1,2,3,4,5], m = 2
Output: 9
```

**Example 3:**

```
Input: nums = [1,4,4], m = 3
Output: 4
```

 

**Constraints:**

- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 106`
- `1 <= m <= min(50, nums.length)`





## 分析

这道题要求这m个子数组各自和的最大值最小，应对数组问题，可以考虑二分搜索，首先要确定上下界。由于各自和的最大值会在max（nums[i]）和sum之间，可以以max为左边界，sum为右边界，利用二分搜索不断接近并得到答案。

在分割时，采用mid=（l+r）/2要确保数字总和足够大，而又小于结果之间。

我们会得到两种结果：

1.我们可以将数组分成m个以上子数列，这样，意味着我们的中间值太小，因此可以将l=mid+1;

2.不可以分成m个数列，这样说明中间值过大，可以将r=mid-1;

#### 方法

采用二分搜索的方法，不断遍历，直至左右边界相遇

#### 代码

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int max=0;long sum=0;
        for(int num:nums) {
            max=Math.max(max,num);
            sum+=num;
        }
        if(m==1) return (int)sum;
        long l=max;long r=sum;
        while(l<=r) {
            long mid=(l+r)/2;
            if(valid(mid,nums,m)) {
                r=mid-1;
            } else {
                l=mid+1;
            }
        }
        return (int)l;
    }
    public boolean valid(long target,int[] nums,int m) {
        int count=1;
        long total=0;
        for(int num:nums) {
            total+=num;
            if(total>target) {
                total=num;
                count++;
                if(count>m) {
                    return false;
                }
            }
        }
        return true;
    }
}
```

