---
title: Leetcode 541. Reverse String II 反转字符串 II
author: Mark
summary: 设置一个左端点i和右端点i+k-1，构建reverse函数，反转左端点和右端点之间的字符即可
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: e834e913
date: 2021-09-27 19:53:00
---

Given a string `s` and an integer `k`, reverse the first `k` characters for every `2k` characters counting from the start of the string.

If there are fewer than `k` characters left, reverse all of them. If there are less than `2k` but greater than or equal to `k` characters, then reverse the first `k` characters and left the other as original.

 

**Example 1:**

```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

**Example 2:**

```
Input: s = "abcd", k = 2
Output: "bacd"
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of only lowercase English letters.
- `1 <= k <= 104`



## 分析

1.每隔k个字符，则反转k个字符串，可以设置一个左端点i和右端点i+k-1

2.构建reverse函数，反转左端点和右端点之间的字符即可

#### 方法

设置左右端点，遍历并反转字符

#### 代码

```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] array=s.toCharArray();
        for(int i=0;i<s.length();) {
            int j=Math.min(i+k-1,s.length()-1);
            swap(i,j,array);
            i=i+2*k;
        }
        return String.valueOf(array);
    }
    public void swap(int i,int j,char[] array) {
        while(i<j) {
            char temp=array[i];
            array[i]=array[j];
            array[j]=temp;
            i++;j--;
        }
    }
}
```

