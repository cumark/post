---
title: Leetcode 221. Maximal Square 最大正方形
author: Mark
summary: 使用dp二维数组，储存i行j列之下的dp值，对行列进行遍历，并进行更新，求得最大的面积值
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 15:24:00
---
Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

 
Example 1:

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211012151628.png)
```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4
```
Example 2:

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211012151648.png)
Input: matrix = [["0","1"],["1","0"]]
Output: 1
Example 3:

```
Input: matrix = [["0"]]
Output: 0
``` 

Constraints:

+ m == matrix.length
+ n == matrix[i].length
+ 1 <= m, n <= 300
+ matrix[i][j] is '0' or '1'.


## 分析

1.二维矩阵问题，优先考虑使用动态规划解决

2.这里求正方形最小面积，正方形从左下角，遍历至右上角，可以推出动态规划方程`dp[i][j]=Math.min(Math.min(dp[i-1][j-1],dp[i-1][j]),dp[i][j-1])+1`

3.每一步都更新，使得res等于过程中最大的面积值

#### 方法

使用dp二维数组，储存i行j列之下的dp值，对行列进行遍历，并进行更新，求得最大的面积值


#### 代码

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        int m=matrix.length;
        int n=matrix[0].length;int result=0;
        int[][] dp=new int[m+1][n+1];
        for(int i=1;i<=m;i++) {
            for(int j=1;j<=n;j++) {
                if(matrix[i-1][j-1]=='1') {
                    dp[i][j]=Math.min(Math.min(dp[i-1][j-1],dp[i-1][j]),dp[i][j-1])+1;
                }
                result=Math.max(result,dp[i][j]);
            }
        }
        return result*result;
    }
}
```

