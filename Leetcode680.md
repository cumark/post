---
title: Leetcode 680. Valid Palindrome II 验证回文子串II
author: Mark
summary: >-
  一个字符串在允许删掉一个字符的情况下，是否能成为回文串，由于回文子串的特性是首位相同，因此采用双指针方法解决问题。当双指针前后遍历字符串，遇到前后所指字符不同的情况时，有两种可能性，删除前指针或后指针所指的字符，那么可以采用||运算符。
tags:
  - leetcode
  - algorithm
  - pointer
categories:
  - 算法
abbrlink: 190801a7
date: 2021-09-26 12:30:00
---

Given a string `s`, return `true` *if the* `s` *can be palindrome after deleting **at most one** character from it*.

 

**Example 1:**

```
Input: s = "aba"
Output: true
```

**Example 2:**

```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```

**Example 3:**

```
Input: s = "abc"
Output: false
```

 

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of lowercase English letters.



## 分析

这道题求一个字符串在允许删掉一个字符的情况下，是否能成为回文串，由于回文子串的特性是首位相同，因此采用双指针方法解决问题。当双指针前后遍历字符串，遇到前后所指字符不同的情况时，有两种可能性，删除前指针或后指针所指的字符，那么可以采用||运算符。

#### 方法

双指针遍历字符，若遇到不同的字符，则转到删除前或后指针所指字符后的判断函数。

#### 代码

```java
class Solution {
    public boolean validPalindrome(String s) {
        int l=0;int r=s.length()-1;
        while(l<r) {
            if(s.charAt(l)==s.charAt(r)) {
                l++;
                r--;
            } else {
                return func(s,l+1,r)||func(s,l,r-1);
            }
        }
        return true;
    }
    public boolean func(String s,int l,int r) {
        while(l<r) {
            if(s.charAt(l)==s.charAt(r)) {
                l++;
                r--;
            } else {
                return false;
            }
        }
        return true;
    }
}
```

