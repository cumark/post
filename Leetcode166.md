---
title: Leetcode 166. Fraction to Recurring Decimal 分数到小数
author: Mark
summary: 首先让被除数除以除数，得到余数，再让余数乘十，迭代这个过程，直到整除或者出现循环
tags:
  - leetcode
  - algorithm
categories:
  - 算法
date: 2021-10-04 20:09:00
---

Given two integers representing the `numerator` and `denominator` of a fraction, return *the fraction in string format*.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return **any of them**.

It is **guaranteed** that the length of the answer string is less than `104` for all the given inputs.

 

**Example 1:**

```
Input: numerator = 1, denominator = 2
Output: "0.5"
```

**Example 2:**

```
Input: numerator = 2, denominator = 1
Output: "2"
```

**Example 3:**

```
Input: numerator = 2, denominator = 3
Output: "0.(6)"
```

**Example 4:**

```
Input: numerator = 4, denominator = 333
Output: "0.(012)"
```

**Example 5:**

```
Input: numerator = 1, denominator = 5
Output: "0.2"
```

 

**Constraints:**

- `-231 <= numerator, denominator <= 231 - 1`
- `denominator != 0`


## 分析

1.将分数转化为小数，是一个古老且有意义的问题。首先要明确一个数学概念，分数转化为小数，当小数出现与之前相同的数字，则为循环

2.小数采用的是十进制计数，可以将余数乘十，再进行拼接

3.将每一个小数数值与小数目前的长度映射，当出现与当前小数数字相同的数字时，即在映射的位置和最后加入括号


#### 方法

首先让被除数除以除数，得到余数，再让余数乘十，迭代这个过程，直到整除或者出现循环


#### 代码

```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if(numerator==0) {
            return "0";
        }
        StringBuilder ans=new StringBuilder();
        ans.append((numerator>0)^(denominator>0)?"-":"");
        long num=Math.abs((long)numerator);
        long den=Math.abs((long)denominator);
        ans.append(num/den);
        if(num%den==0) {
            return ans.toString();
        } else {
            num%=den;
        }
        ans.append(".");
        HashMap<Long,Integer> map=new HashMap();
        map.put(num,ans.length());
        while(num!=0) {
            num*=10;
            ans.append(num/den);
            num%=den;
            if(map.containsKey(num)) {
                int index=map.get(num);
                ans.insert(index,"(");
                ans.append(")");
                break;
            } else {
                map.put(num,ans.length());
            }
        }
        return ans.toString();
    }
}
```

