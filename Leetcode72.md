---
title: Leetcode 72. Edit Distance 编辑距离
author: Mark
summary: 使用动态规划方法，动态规划方程为`dp[i][j]=Math.min(dp[i-1][j],Math.min(dp[i][j-1],dp[i-1][j-1]))+1`(word1.charAt(i-1)!=word2.charAt(i-1))
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 16:54:00
---
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

Insert a character
Delete a character
Replace a character
 

Example 1:

```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```
Example 2:

```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

Constraints:

+ 0 <= word1.length, word2.length <= 500
+ word1 and word2 consist of lowercase English letters.

## 分析

1.针对字符串问题，优先考虑使用动态规划方法

2.使用二维数组，记录word1前i个字符和word2前j个字符要编辑所需的距离

3.对于边界问题，当i或j等于0时，那么`dp[i][0]`或`dp[0][i]`等于i

4.动态规划方程为`dp[i][j]=Math.min(dp[i-1][j],Math.min(dp[i][j-1],dp[i-1][j-1]))+1`(word1.charAt(i-1)!=word2.charAt(i-1))

#### 方法

使用动态规划方法，动态规划方程为`dp[i][j]=Math.min(dp[i-1][j],Math.min(dp[i][j-1],dp[i-1][j-1]))+1`(word1.charAt(i-1)!=word2.charAt(i-1))

#### 代码

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m=word1.length();
        int n=word2.length();
        int[][] dp=new int[m+1][n+1];
        for(int i=0;i<=m;i++) {
            dp[i][0]=i;
        }
        for(int i=0;i<=n;i++) {
            dp[0][i]=i;
        }
        for(int i=1;i<=m;i++) {
            for(int j=1;j<=n;j++) {
                if(word1.charAt(i-1)==word2.charAt(j-1)) {
                    dp[i][j]=dp[i-1][j-1];
                }else {
                    dp[i][j]=Math.min(dp[i-1][j],Math.min(dp[i][j-1],dp[i-1][j-1]))+1;
                }
            }
        }
        return dp[m][n];
    }
}
```

