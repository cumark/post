---
title: "Leetcode 326. Power of Three 3的幂"
author: Mark
summary: 使用数学约数方法解决3的幂问题
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: 3e4049d7
date: 2021-09-22 14:37:00
---

Given an integer `n`, return *`true` if it is a power of three. Otherwise, return `false`*.

An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.

 

**Example 1:**

```
Input: n = 27
Output: true
```

**Example 2:**

```
Input: n = 0
Output: false
```

**Example 3:**

```
Input: n = 9
Output: true
```

**Example 4:**

```
Input: n = 45
Output: false
```

 

**Constraints:**

- `-2^31 <= n <= 2^31 - 1`



### 分析：这道题要判断n是否是3的幂



## 方法一

最容易想到的思路是，用n不断除3，如果能除到1且无余数则为3的幂，否则不是。整个过程的时间复杂度为log(n)，时间复杂度为log(1)

#### 代码

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        while(n!=0&&n%3==0) {
            n/=3;
        }
        return n==1;
    }
}
```

## 方法二

在int可表示的范围内，3的最大幂为3的19次幂，这个数字仅是3的幂数的公倍数，所以可以从n是否3的19次幂的约数来判断。这个过程仅做了常数级运算，时间复杂度为log(1)，空间复杂度为log(1)

#### 代码

```
class Solution {
    public boolean isPowerOfThree(int n) {
        int max=(int)Math.pow(3,19);
        if(n>0&&max%n==0) {
            return true;
        }
        return false;
    }
}
```

