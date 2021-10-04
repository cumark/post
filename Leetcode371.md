---
title: Leetcode 371. Sum of Two Integers 两整数之和
author: Mark
summary: 在不使用+-号及其相关符号的原则下，实现两个整数相加，优先考虑位运算，可以把需要进位和不需要进位的部分迭代运算。
tags:
  - leetcode
  - algorithm
  - bit
categories:
  - 算法
abbrlink: 22becddc
date: 2021-09-25 14:02:00
---

Given two integers `a` and `b`, return *the sum of the two integers without using the operators* `+` *and* `-`.

 

**Example 1:**

```
Input: a = 1, b = 2
Output: 3
```

**Example 2:**

```
Input: a = 2, b = 3
Output: 5
```

 

**Constraints:**

- `-1000 <= a, b <= 1000`

## 分析：

题目的要求非常简单，在不使用+-号及其相关符号的原则下，实现两个整数相加，优先考虑位运算，可以把需要进位和不需要进位的部分迭代运算。



#### 方法

根据以上分析，对于需要进位的部分，用(a&b)<<1实现，对于不需要进位，则用a^b的实现，不断迭代，代码如下：

#### 代码

```java
class Solution {
    public int getSum(int a, int b) {
        while(a!=0) {
            int index=(a&b)<<1;
            b=a^b;
            a=index;
        }
        return b;
    }
}
```

