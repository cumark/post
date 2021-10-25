---
title: Leetcode 414. Third Maximum Number 第三大的数
author: Mark
summary: 设置三个值来记录，并不断更新，若max3不等于mull，返回max3，否则返回max1
tags:
  - leetcode
  - algorithm
categories:
  - 算法
date: 2021-10-12 00:09:00
---
Given an integer array nums, return the third distinct maximum number in this array. If the third maximum does not exist, return the maximum number.

 

Example 1:

```
Input: nums = [3,2,1]
Output: 1
Explanation:
The first distinct maximum is 3.
The second distinct maximum is 2.
The third distinct maximum is 1.
```
Example 2:

```
Input: nums = [1,2]
Output: 2
Explanation:
The first distinct maximum is 2.
The second distinct maximum is 1.
The third distinct maximum does not exist, so the maximum (2) is returned instead.
```
Example 3:

```
Input: nums = [2,2,3,1]
Output: 1
Explanation:
The first distinct maximum is 3.
The second distinct maximum is 2 (both 2's are counted together since they have the same value).
The third distinct maximum is 1.
 ```

Constraints:

+ 1 <= nums.length <= 10^4
+ -2^31 <= nums[i] <= 2^31 - 1



## 分析

1.这道题有2^31-1等边界测试用例，而此时将max1，2，3置为最小值多有不便，可以设置为Integer，初始化为null

2.设置三个数值记录，max1，max2和max3，分别记录第一第二第三个值

3.从第一开始过滤，若大于第一个，或者第一个为null，则第三个等于第二个，第二个等于第一个，其他的也是此逻辑

#### 方法

设置三个值来记录，并不断更新，若max3不等于mull，返回max3，否则返回max1


#### 代码

```java
class Solution {
    public int thirdMax(int[] nums) {
        Integer max1=null;
        Integer max2=null;
        Integer max3=null;
        int flag=0;
        for(Integer num:nums) {
            if(num.equals(max1)||num.equals(max2)||num.equals(max3)) {
                continue;
            }
            if(max1==null||num>max1) {
                max3=max2;
                max2=max1;
                max1=num;
            } else if(max2==null||num>max2) {
                max3=max2;
                max2=num;
            } else if(max3==null||num>max3){
                flag=1;
                max3=num;
            }
        }
        if(max3==null) {
            return max1;
        }
        return max3;
    }
}
```

