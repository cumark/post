---
title: Leetcode 44. Wildcard Matching 通配符匹配
author: Mark
summary: '用动态规划解决问题，通配符在匹配时有三种情况,分别分析，并针对第三种情况分为两类，合并第一、二种情况，构建动态规划方程即可解决问题'
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
abbrlink: '34851722'
date: 2021-09-26 12:02:00
---

Given an input string (`s`) and a pattern (`p`), implement wildcard pattern matching with support for `'?'` and `'*'` where:

- `'?'` Matches any single character.
- `'*'` Matches any sequence of characters (including the empty sequence).

The matching should cover the **entire** input string (not partial).

 

**Example 1:**

```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

**Example 2:**

```
Input: s = "aa", p = "*"
Output: true
Explanation: '*' matches any sequence.
```

**Example 3:**

```
Input: s = "cb", p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

**Example 4:**

```
Input: s = "adceb", p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

**Example 5:**

```
Input: s = "acdcb", p = "a*c?b"
Output: false
```

 

**Constraints:**

- `0 <= s.length, p.length <= 2000`
- `s` contains only lowercase English letters.
- `p` contains only lowercase English letters, `'?'` or `'*'`.

分析：这道题求两个字符串是否匹配，考虑用动态规划解决问题，通配符在匹配时有三种情况，

第一种，s.charAt(i)==p.charAt(j)，那么其能否匹配与`dp[i-1][j-1]`相同

第二种，p.charAt(j)=='?'，这时无论s.charAt(i)的字符为何，皆可以匹配，与`dp[i-1][j-1]`相同

第三种，p.charAt(j)=='*'，这时相关情况可分为两类

​			第一类，*用于表示空格，此时与`dp[i][j-1]`相同

​			第二类，*用于表示一串字符，此时与`dp[i-1][j]`相同

## 方法

根据以上分析，采用动态规划方法，动态规划方程为：

`dp[i][j]=dp[i-1][j-1]`(s.charAt(i)==p.charAt(j)||p.charAt(j)=='?')

`dp[i][j]=dp[i-1][j]||dp[i][j-1])`(p.charAt(j)=='*')，代码如下：

#### 代码

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m=s.length();int n=p.length();
        boolean[][] dp=new boolean[m+1][n+1];
        for(int i=1;i<=m;i++) {
            dp[i-1][0]=false;
        }
        boolean flag=true;
        for(int i=1;i<=n;i++) {
            if(p.charAt(i-1)!='*') {
                flag=false;
            }
            dp[0][i]=flag;
        }
        dp[0][0]=true;
        for(int i=1;i<=m;i++) {
            for(int j=1;j<=n;j++) {
                if(s.charAt(i-1)==p.charAt(j-1)||p.charAt(j-1)=='?') {
                    dp[i][j]=dp[i-1][j-1];
                } else if(p.charAt(j-1)=='*'){
                    dp[i][j]=dp[i-1][j]||dp[i][j-1];
                }
            }
        }
        return dp[m][n];
    }
}
```

