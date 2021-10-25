---
title: Leetcode 403. Frog Jump 青蛙过河
author: Mark
summary: 动态规划方程为`dp[i][k]=dp[j][k-1]||dp[j][k]||dp[j][k+1]`，边界`dp[0][0]`为true，最后，只要`dp[n-1][i]`i为任意值为true即可过河
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-11 00:19:00
---

A frog is crossing a river. The river is divided into some number of units, and at each unit, there may or may not exist a stone. The frog can jump on a stone, but it must not jump into the water.

Given a list of stones' positions (in units) in sorted ascending order, determine if the frog can cross the river by landing on the last stone. Initially, the frog is on the first stone and assumes the first jump must be 1 unit.

If the frog's last jump was k units, its next jump must be either k - 1, k, or k + 1 units. The frog can only jump in the forward direction.

 

Example 1:

```
Input: stones = [0,1,3,5,6,8,12,17]
Output: true
Explanation: The frog can jump to the last stone by jumping 1 unit to the 2nd stone, then 2 units to the 3rd stone, then 2 units to the 4th stone, then 3 units to the 6th stone, 4 units to the 7th stone, and 5 units to the 8th stone.
```
Example 2:

```
Input: stones = [0,1,2,3,4,8,9,11]
Output: false
Explanation: There is no way to jump to the last stone as the gap between the 5th and 6th stone is too large.
```

Constraints:

+ 2 <= stones.length <= 2000
+ 0 <= stones[i] <= 2^31 - 1
+ stones[0] == 0
+ stones is sorted in a strictly increasing order.

## 分析

1.使用动态规划方法解决该问题，dp[i][j]表示第i个位置且上一次跳跃距离为j是否可以通过

2.动态规划方程为`dp[i][k]=dp[j][k-1]||dp[j][k]||dp[j][k+1]`，其中j为与i有一跳距离的地方，有三种可能，0，+1，-1

3.当i不变，j遍历时，由于间隔过大时（k>j+1），需停止遍历，故，逆序遍历

4.由于i依靠于j的dp值，而i大于j，故i顺序遍历即可

5.对于边界，`dp[0][0]`为true，要有起始的true

6.做预先判断，由于每一跳只能加1，所以如果两石头之和大于i，则返回false

7.最后，只要`dp[n-1][i]`i为任意值为true即可过河


#### 方法

动态规划方程为`dp[i][k]=dp[j][k-1]||dp[j][k]||dp[j][k+1]`，边界`dp[0][0]`为true，最后，只要`dp[n-1][i]`i为任意值为true即可过河

#### 代码

```java
class Solution {
    public boolean canCross(int[] stones) {
        int n=stones.length;
        boolean[][] dp=new boolean[n][n];
        dp[0][0]=true;
        for(int i=1;i<n;i++) {
            if(stones[i]-stones[i-1]>i) {
                return false;
            }
        }
        for(int i=1;i<n;i++) {
            for (int j=i-1;j>=0;j--) {
                int k=stones[i]-stones[j];
                if(k>j+1) {
                    break;
                }
                dp[i][k]=dp[j][k-1]||dp[j][k]||dp[j][k+1];
            }
        }
        for(int i=0;i<n;i++) {
            if(dp[n-1][i])
                return true;
        }
        return false;
    }
}
```

