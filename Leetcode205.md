---
title: Leetcode 205. Isomorphic Strings 同构字符串
author: Mark
summary: 这道题要求判断两个字符串是否具有相同的结构，在遍历过程中，如果遍历到两个字符串中的字符，上一次出现的位置不同，那么可以判定它们是不同结构的
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: 3d60dd91
date: 2021-09-26 23:01:00
---

Given two strings `s` and `t`, *determine if they are isomorphic*.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

 

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true
```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false
```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true
```



分析：这道题要求判断两个字符串是否具有相同的结构，在遍历过程中，如果遍历到两个字符串中的字符，上一次出现的位置不同，那么可以判定它们是不同结构的

## 方法

初始化两个空间为256的数组，遍历到两个字符串中的字符，上一次出现的位置不同，那么可以判定它们是不同结构的

#### 代码

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int[] m1=new int[256];
        int[] m2=new int[256];
        for(int i=0;i<s.length();i++) {
            if(m1[s.charAt(i)]!=m2[t.charAt(i)])
                return false;
            else {
                m1[s.charAt(i)]=i+1;
                m2[t.charAt(i)]=i+1;
            }
        }
        return true;
    }
}
```

