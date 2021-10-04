---
title: Leetcode 58. Length of Last Word 最后一个单词的长度
author: Mark
summary: 这道题求一个句子之中最后一个单词的长度，最简单的方法就是判断是不是为空格，是空格就把sum置0，否则累加，最终得到的就是最后一个单词的长度
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: 776c8164
date: 2021-09-23 20:31:00
---

Given a string `s` consisting of some words separated by some number of spaces, return *the length of the **last** word in the string.*

A **word** is a maximal substring consisting of non-space characters only.

 

**Example 1:**

```
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

**Example 2:**

```
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```

**Example 3:**

```
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of only English letters and spaces `' '`.
- There will be at least one word in `s`.



分析：这道题求一个句子之中最后一个单词的长度，最简单的方法就是判断是不是为空格，是空格就把sum置0，否则累加，最终得到的就是最后一个单词的长度



## 方法

遇到空格就把sum置0，否则累加，最终得到最后一个单词的长度

#### 代码

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int sum=0;int ans=0;
        for(char ch:s.toCharArray()) {
            if(ch!=' ') {
                sum++;
                ans=sum;
            } else {
                sum=0;
            }
        }
        return ans;
    }
}
```

