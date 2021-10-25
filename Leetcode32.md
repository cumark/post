---
title: Leetcode 32. Longest Valid Parentheses 最长有效括号
author: Mark
summary: 使用动态规划方程，问题的关键在于，意识到dp[i-dp[i]]记录的便是与i连续有效括号之前的有效括号数量，两者相加即为结果
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 15:37:00
---
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

 

Example 1:

```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
```
Example 2:

```
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```
Example 3:

```
Input: s = ""
Output: 0
```

Constraints:

+ 0 <= s.length <= 3 * 104
+ s[i] is '(', or ')'.


## 分析

1.字符串问题，优先考虑动态规划方法

2.题目要求连续有效的括号，dp[i]记录的是和i连续的有效括号的数量，那么dp[i-dp[i]]记录的便是与i连续有效括号之前的有效括号数量，两者相加即为结果

3.设置一个count，记录左括号的数量，只有count>0时，出现右括号才是有效的括号，使用res记录这个过程中最大的有效连续括号数量

#### 方法

使用动态规划方程，问题的关键在于，意识到dp[i-dp[i]]记录的便是与i连续有效括号之前的有效括号数量，两者相加即为结果

#### 代码

```java
class Solution {
    public int longestValidParentheses(String s) {
        int[] dp=new int[s.length()];
        int res=0;
        int count=0;
        for(int i=0;i<s.length();i++) {
            if(s.charAt(i)=='(') {
                count++;
            } else if(count>0) {
                dp[i]=dp[i-1]+2;
                dp[i]+=(i-dp[i])>=0?dp[i-dp[i]]:0;
                res=Math.max(res,dp[i]);
                count--;
            }
        }
        return res;
    }
}
```

