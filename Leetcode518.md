---
title: Leetcode 518. Longest Valid Parentheses 零钱兑换 II
author: Mark
summary: 使用动态规划方法，一级遍历coins数组，二级遍历amount
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 15:54:00
---
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return 0.

You may assume that you have an infinite number of each kind of coin.

The answer is guaranteed to fit into a signed 32-bit integer.

 

Example 1:

```
Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```
Example 2:

```
Input: amount = 3, coins = [2]
Output: 0
Explanation: the amount of 3 cannot be made up just with coins of 2.
```
Example 3:

```
Input: amount = 10, coins = [10]
Output: 1
```

Constraints:

+ 1 <= coins.length <= 300
+ 1 <= coins[i] <= 5000
+ All the values of coins are unique.
+ 0 <= amount <= 5000

## 分析

1.这道题是求对于总的amount，coins数组有多少种组合

2.可以遍历coins数组，并二级遍历总数，得出动态规划方程`dp[i]+=dp[i-coin]`

#### 方法

使用动态规划方法，一级遍历coins数组，二级遍历amount

#### 代码

```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp=new int[amount+1];
        dp[0]=1;
        for(int coin:coins) {
            for(int i=coin;i<=amount;i++) {
                dp[i]+=dp[i-coin];
            }
        }
        return dp[amount];
    }
}
```

