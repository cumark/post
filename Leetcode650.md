---
title: Leetcode 650. 2 Keys Keyboard 只有两个键的键盘
author: Mark
summary: '看到字符串优先用动态规划方法，确定动态规划公式dp[i]=dp[j]+i/j，确定最终结果'
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: c4b7fa82
date: 2021-09-23 18:54:00
---

- There is only one character `'A'` on the screen of a notepad. You can perform two operations on this notepad for each step:

  - Copy All: You can copy all the characters present on the screen (a partial copy is not allowed).
  - Paste: You can paste the characters which are copied last time.

  Given an integer `n`, return *the minimum number of operations to get the character* `'A'` *exactly* `n` *times on the screen*.

   

  **Example 1:**

  ```
  Input: n = 3
  Output: 3
  Explanation: Intitally, we have one character 'A'.
  In step 1, we use Copy All operation.
  In step 2, we use Paste operation to get 'AA'.
  In step 3, we use Paste operation to get 'AAA'.
  ```

  **Example 2:**

  ```
  Input: n = 1
  Output: 0
  ```

   

  **Constraints:**

  - `1 <= n <= 1000`



## 分析

这道题主要说，如果要从A获得AA，需要2个额外的步骤（全部复制然后粘贴），如果要从A获得AAA，我们需要三个额外的步骤，（全部复制，然后粘贴，再次粘贴）。为了生成 AAAA，我们需要 AA 的 2 个步骤。
但是，要获得 AAAAAAAA，最好的方法是从 AAAA 获得，有 2 个步骤（全部复制然后粘贴）
本质上，我们找到了下一个更短的序列，它可以被复制然后多次粘贴以生成所需的序列。当我们找到一个可以完美分割我们所需序列长度的长度时，我们就不需要检查任何更短的序列。



#### 方法

看到字符串相关，最容易想到的便是动态规划，动态规划方程经验证可写为，dp[i]=dp[j]+i/j，其中dp[i]是目前得到记事本相应字符个数所需的最少操作次数，dp[j]为之前（最终匹配到的为i的约数）。如i=9，j=3，那么经此动态规划方程运算，则dp[i]会在dp[j]的基础上加3，相当于复制，粘贴，粘贴。

#### 代码

```java
class Solution {
    public int minSteps(int n) {
        int[] dp=new int[n+1];
        for(int i=2;i<=n;i++) {
            dp[i]=i;
            for(int j=i-1;j>1;j--) {
                if(i%j==0) {
                    dp[i]=dp[j]+i/j;
                    break;
                }
            }
        }
        return dp[n];
    }
}
```

