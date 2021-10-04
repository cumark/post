---
title: Leetcode 5. Longest Palindromic Substring 最长回文子串
author: Mark
summary: >-
  运用动态规划方法，动态规划方程为，当s.charAt(i)==s.charAt(j)时，这时`dp[i][j]=dp[i-1][j+1]`，当i-j<3时，这时`dp[i][j]=dp[i-1][j+1]`
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
abbrlink: b707e9b2
date: 2021-09-27 20:20:00
---

Given a string `s`, return *the longest palindromic substring* in `s`.

 

**Example 1:**

```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```
Input: s = "a"
Output: "a"
```

**Example 4:**

```
Input: s = "ac"
Output: "a"
```

 

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.





## 分析

字符串问题，优先考虑动态规划的方法。设置`boolean[][] dp`，在遍历时有如下几种情况

+ 当s.charAt(i)==s.charAt(j)时，这时`dp[i][j]=dp[i-1][j+1]`
+ 当i-j<3时，这时`dp[i][j]=dp[i-1][j+1]`

这时会产生一个新的问题，就是需要先遍历以j，i为边界的区间之内明确的boolean判定值，那么采取i正向遍历，j以i为起点逆向遍历，是一个比较好的方式

如果`dp[i][j]`为true并且当前i-j+1>所存结果的长度时，用string.substring来更新所存结果

#### 方法

运用动态规划方法，动态规划方程为，当s.charAt(i)==s.charAt(j)时，这时`dp[i][j]=dp[i-1][j+1]`，当i-j<3时，这时`dp[i][j]=dp[i-1][j+1]`，并不断更新最长的子串

#### 代码

```java
class Solution {
    public String longestPalindrome(String s) {
        int n=s.length();String ans="";
        boolean[][] dp=new boolean[n][n];
        for(int i=0;i<n;i++) {
            for(int j=i;j>=0;j--) {
                if(s.charAt(i)==s.charAt(j))
                    dp[i][j]=(i-j<3||dp[i-1][j+1]);
                if(dp[i][j]&&i-j+1>ans.length()) {
                    ans=s.substring(j,i+1);
                }
            }
        }
        return ans;
    }
}
```

