---
title: Leetcode 517. Super Washing Machines 超级洗衣机
author: Mark
summary: 采用贪心算法，计算平均数，遍历数组，不断更新转移次数
tags:
  - leetcode
  - algorithm
  - greedy
categories:
  - 算法
date: 2021-10-04 19:17:00
---

You have n super washing machines on a line. Initially, each washing machine has some dresses or is empty.

For each move, you could choose any m (1 <= m <= n) washing machines, and pass one dress of each washing machine to one of its adjacent washing machines at the same time.

Given an integer array machines representing the number of dresses in each washing machine from left to right on the line, return the minimum number of moves to make all the washing machines have the same number of dresses. If it is not possible to do it, return -1.

 

Example 1:

```
Input: machines = [1,0,5]
Output: 3
Explanation:
1st move:    1     0 <-- 5    =>    1     1     4
2nd move:    1 <-- 1 <-- 4    =>    2     1     3
3rd move:    2     1 <-- 3    =>    2     2     2
```
Example 2:

```
Input: machines = [0,3,0]
Output: 2
Explanation:
1st move:    0 <-- 3     0    =>    1     2     0
2nd move:    1     2 --> 0    =>    1     1     1
```
Example 3:

```
Input: machines = [0,2,0]
Output: -1
Explanation:
It's impossible to make all three washing machines have the same number of dresses.
 ```

Constraints:

```
n == machines.length
1 <= n <= 104
0 <= machines[i] <= 105
```


## 分析

1.将该问题简化
+ 拿到较多衣服的洗衣机把衣服转移到较少衣服的洗衣机之中，最终实现平均
+ 由于转移衣服的过程中，只能往周围转移，实现在此过程可以从前到后遍历

2.用sum统计每一个洗衣机的衣服数量和平均数之间的差值，若大于遍历到的num及之前统计到的数值，则sum即为转移次数


#### 方法

采用贪心算法，计算平均数，遍历数组，不断更新转移次数


#### 代码

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        int total=Arrays.stream(machines).sum();
        int n=machines.length;
        if(total%n!=0) {
            return -1;
        }
        int aver=total/n;
        int ans=0;int sum=0;
        for(int num:machines) {
            num-=aver;
            sum+=num;
            ans=Math.max(ans,Math.max(num,Math.abs(sum)));
        }
        return ans;
    }
}
```

