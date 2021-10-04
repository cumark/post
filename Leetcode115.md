---
title: Leetcode 115. Distinct Subsequences 两个字符串的删除操作
author: Mark
summary: >-
  采用动态规划方程方法解题，动态规划方程为：`dp[i][j]=dp[i-1][j-1]+dp[i-1][j](s.charAt(i)==t.charAt[j]),dp[i][j]=dp[i-1][j](s.charAt(i)!=t.charAt(j))`
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
abbrlink: 973b595
date: 2021-09-25 14:02:00
---

Given two strings s and t, return the number of distinct subsequences of s which equals t.

A string's subsequence is a new string formed from the original string by deleting some (can be none) of the characters without disturbing the remaining characters' relative positions. (i.e., "ACE" is a subsequence of "ABCDE" while "AEC" is not).

It is guaranteed the answer fits on a 32-bit signed integer.

 

Example 1:
```
Input: s = "rabbbit", t = "rabbit"
Output: 3
Explanation:
As shown below, there are 3 ways you can generate "rabbit" from S.
rabbbit
rabbbit
rabbbit
```
Example 2:
```
Input: s = "babgbag", t = "bag"
Output: 5
Explanation:
As shown below, there are 5 ways you can generate "bag" from S.
babgbag
babgbag
babgbag
babgbag
babgbag
```

Constraints:

1 <= s.length, t.length <= 1000
s and t consist of English letters.

分析：

这道题求字符串t在字符串s中出现的个数，看到字符串的个数求解，考虑用动态规划去解决问题。一级遍历字符串s，二级遍历t时，当s.charAt(i)==t.charAt(j)时，这时会出现两种情况，一种是，t中新出现的t.charAt(i)对于结果无影响，那么让其等于上一层即可,即`dp[i][j]=dp[i-1][j-1]`，第二种是，t中新出现的t.charAt(i)对于结在s的0—（i-1）之中存在,`dp[i][j]=dp[i-1][j]`。

如果s.charAt(i)!=t.charAt(j)那么上文中的第一种条件将不可能存在，那么只有第二种，即

`dp[i][j]=dp[i-1][j]`



## 方法

根据以上分析，采用动态规划方法，动态规划方程为：`dp[i][j]=dp[i-1][j-1]+dp[i-1][j](s.charAt(i)==t.charAt[j]),dp[i][j]=dp[i-1][j](s.charAt(i)!=t.charAt(j))`，代码如下：

#### 代码

```java
class Solution {
    public int numDistinct(String s, String t) {
        int m=s.length();int n=t.length();
        int[][] dp=new int[m+1][n+1];
        if(m<n) {
            return 0;
        }
        for(int i=0;i<=m;i++) {
            dp[i][0]=1;
        }
        for(int i=1;i<=m;i++) {
            for(int j=1;j<=n;j++) {
                if(s.charAt(i-1)==t.charAt(j-1)) {
                    dp[i][j]=dp[i-1][j-1]+dp[i-1][j];
                } else {
                    dp[i][j]=dp[i-1][j];
                }
            }
        }
        return dp[m][n];
    }
}
```

