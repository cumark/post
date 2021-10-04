---
title: Leetcode 673. Number of Longest Increasing Subsequence 最长递增子序列的个数
author: Mark
summary: 使用动态规划方法，限定词为最长，可以设置为一个dp数组，递增放到循环里进行判断，故设置len[i]表示结尾为nums[i]的最长子序列的长度，cnt[i]表示结尾为nums[i]的最长子序列的数量。
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: e88ed89b
date: 2021-09-23 20:04:00
---

Given an integer array `nums`, return *the number of longest increasing subsequences.*

**Notice** that the sequence has to be **strictly** increasing.

 

**Example 1:**

```
Input: nums = [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].
```

**Example 2:**

```
Input: nums = [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

 

**Constraints:**

- `1 <= nums.length <= 2000`
- `-10^6 <= nums[i] <= 10^6`

分析：这道题给出一个数组，要求求出最长的递增的子序列的总数，这里有两个限定词，最长和递增。题目为求总数，可以用动态规划方法，限定词为最长，可以设置为一个dp数组，递增放到循环里进行判断，故设置len[i]表示结尾为nums[i]的最长子序列的长度，cnt[i]表示结尾为nums[i]的最长子序列的数量。



## 方法

对于数组中或中的每个元素，它们都带有三个字段：
1）最大增加/减少长度以当前元素结束，
2）它自己的值，
3）最大长度的总数，
并且每次我们访问一个元素时，我们都会使用它来更新1和 3
设置len[i]表示结尾为nums[i]的最长子序列的长度，cnt[i]表示结尾为nums[i]的最长子序列的数量。

#### 代码

```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        int n=nums.length;
        int ans=0;int max=0;
        int[] len=new int[n];//长度
        int[] cnt=new int[n];//个数
        for(int i=0;i<n;i++) {
            len[i]=cnt[i]=1;
            for(int j=0;j<i;j++) {
                if(nums[i]>nums[j]) {
                    if(len[i]==len[j]+1) {
                        cnt[i]+=cnt[j];
                    } else if(len[i]<len[j]+1) {
                        len[i]=len[j]+1;
                        cnt[i]=cnt[j];
                    }
                }
            }
            //求最大递增子序列的数量
            if(max==len[i]) {
                ans+=cnt[i];
            }
            if(max<len[i]) {
                ans=cnt[i];
                max=len[i];
            }
        }
        return ans;
    }
}
```

