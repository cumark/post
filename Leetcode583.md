---
title: Leetcode 583. Delete Operation for Two Strings 两个字符串的删除操作
author: Mark
summary: >-
  求找到使得word1和word2相同所需的最小步数，每步可以删除一个字符。字符串相关的问题，首先考虑动态规划，当遍历word1和word2时，有两种可能性情况
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
abbrlink: 345fb18b
date: 2021-09-25 14:02:00

---

Given two strings word1 and word2, return the minimum number of steps required to make word1 and word2 the same.

In one step, you can delete exactly one character in either string.


Example 1:

```
Input: word1 = "sea", word2 = "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

Example 2:

```
Input: word1 = "leetcode", word2 = "etco"
Output: 4
```

Constraints:

1 <= word1.length, word2.length <= 500
word1 and word2 consist of only lowercase English letters.

## 分析

这道题求找到使得word1和word2相同所需的最小步数，每步可以删除一个字符。字符串相关的问题，首先考虑动态规划，当遍历word1和word2时，有两种可能性情况，第一种：word1.charAt(i)==word2.charAt(j)，第二种：word1.charAt(i)!=word2.charAt(j)



#### 方法

采用动态规划方法，动态规划方程为：`dp[i][j]=dp[i-1][j-1](word(i)==word[j]),dp[i][j]=Math.min(dp[i-1][j],dp[i][j-1])+1(word[i]!=word[j])，`代码如下：

#### 代码

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp=new int[word1.length()+1][word2.length()+1];
        for(int i=0;i<word1.length()+1;i++) {
            dp[i][0]=i;
        }
        for(int i=0;i<word2.length()+1;i++) {
            dp[0][i]=i;
        }
        for(int i=1;i<word1.length()+1;i++) {
            for(int j=1;j<word2.length()+1;j++) {
                if(word1.charAt(i-1)==word2.charAt(j-1)) {
                    dp[i][j]=dp[i-1][j-1];
                }
                if(word1.charAt(i-1)!=word2.charAt(j-1)) {
                    dp[i][j]=Math.min(dp[i-1][j],dp[i][j-1])+1;
                }
            }
        }
        return dp[word1.length()][word2.length()];
    }
}
```

