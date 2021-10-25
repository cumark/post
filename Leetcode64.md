---
title: Leetcode 64. Minimum Path Sum 最小路径和
author: Mark
summary: 使用动态规划方程，动态规划方程为`dp[i][j]=grid[i][j]+Math.min(dp[i][j-1],dp[i-1][j])`
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 15:37:00
---
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

 

Example 1:

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211012153919.png)
```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```
Example 2:

```
Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```

Constraints:

+ m == grid.length
+ n == grid[i].length
+ 1 <= m, n <= 200
+ 0 <= grid[i][j] <= 100


## 分析

1.这是一道入门的动态规划问题，非常经典

2.由于是二维矩阵，设置二位数组记录行列数据，对于边界，进行累加即可

3.动态规划方程为`dp[i][j]=grid[i][j]+Math.min(dp[i][j-1],dp[i-1][j])`

#### 方法

使用动态规划方程，动态规划方程为`dp[i][j]=grid[i][j]+Math.min(dp[i][j-1],dp[i-1][j])`

#### 代码

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m=grid.length;
        int n=grid[0].length;
        int[][] dp=new int[m][n];
        dp[0][0]=grid[0][0];
        for(int i=1;i<m;i++) {
            dp[i][0]=grid[i][0]+dp[i-1][0];
        }
        for(int i=1;i<n;i++) {
            dp[0][i]=grid[0][i]+dp[0][i-1];
        }
        for(int i=1;i<m;i++) {
            for(int j=1;j<n;j++) {
                dp[i][j]=grid[i][j]+Math.min(dp[i][j-1],dp[i-1][j]);
            }
        }
        return dp[m-1][n-1];
    }
}
```

