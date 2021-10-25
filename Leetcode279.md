---
title: Leetcode 279. Perfect Squares 完全平方数
author: Mark
summary: 使用动态规划方法，动态规划方程为`dp[i+j*j]=Math.min(dp[i+j*j],dp[i]+1)`
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 16:54:00
---
Given an integer n, return the least number of perfect square numbers that sum to n.

A perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, 1, 4, 9, and 16 are perfect squares while 3 and 11 are not.

 

Example 1:

```
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```
Example 2:

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

Constraints:

+ 1 <= n <= 10^4

## 分析

1.完全平方数可以由前到后，以递推的形式得出结果，采用动态规范方式

2.对于dp初始值，因为要和dp[i]+1相对比，那么dp[0]=0，其他的置为最大值

3.动态规划方程为`dp[i+j*j]=Math.min(dp[i+j*j],dp[i]+1)`

#### 方法

使用动态规划方法，动态规划方程为`dp[i+j*j]=Math.min(dp[i+j*j],dp[i]+1)`

#### 代码

```java
class Solution {
    public int numSquares(int n) {
        int[] dp=new int[n+1];
        Arrays.fill(dp,Integer.MAX_VALUE);
        dp[0]=0;
        for(int i=0;i<=n;i++) {
            for(int j=1;i+j*j<=n;j++) {
                dp[i+j*j]=Math.min(dp[i+j*j],dp[i]+1);
            }
        }
        return dp[n];
    }
}
```

