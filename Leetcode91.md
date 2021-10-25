---
title: Leetcode 91. Decode Ways 解码方法
author: Mark
summary: 使用dp一维数组，当s.charAt(i)！=0时，首先可以确定，dp[i]=dp[i+1]，其次，如果这个值和上一位凑成的两位数为10以上及26以下的数值，则，解码可以增加dp[i+2]
tags:
  - leetcode
  - algorithm
  - dp
categories:
  - 算法
date: 2021-10-12 15:24:00
---
A message containing letters from A-Z can be encoded into numbers using the following mapping:

'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
To decode an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, "11106" can be mapped into:

"AAJF" with the grouping (1 1 10 6)
"KJF" with the grouping (11 10 6)
Note that the grouping (1 11 06) is invalid because "06" cannot be mapped into 'F' since "6" is different from "06".

Given a string s containing only digits, return the number of ways to decode it.

The answer is guaranteed to fit in a 32-bit integer.

 

Example 1:

```
Input: s = "12"
Output: 2
Explanation: "12" could be decoded as "AB" (1 2) or "L" (12).
```
Example 2:

```
Input: s = "226"
Output: 3
Explanation: "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```
Example 3:

```
Input: s = "0"
Output: 0
Explanation: There is no character that is mapped to a number starting with 0.
The only valid mappings with 0 are 'J' -> "10" and 'T' -> "20", neither of which start with 0.
Hence, there are no valid ways to decode this since all digits need to be mapped.
```
Example 4:

```
Input: s = "06"
Output: 0
Explanation: "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").
```
 

Constraints:

+ 1 <= s.length <= 100
+ s contains only digits and may contain leading zero(s).


## 分析

1.字符串解码问题，考虑用动态规划解决问题

2.由于有前置0的存在，所以可以从后往前进行遍历，边界值dp[n]可以设置为1

3.当s.charAt(i)！=0时，首先可以确定，dp[i]=dp[i+1]，其次，如果这个值和上一位凑成的两位数为10以上及26以下的数值，则，解码可以增加dp[i+2]

#### 方法

使用动态规划解决该问题，动态规划方程为
```
            if(s.charAt(i)!='0') {
                dp[i]=dp[i+1];
                if(i<n-1&&(s.charAt(i)=='1'||s.charAt(i)=='2'&&s.charAt(i+1)<'7'))
                    dp[i]+=dp[i+2];
            }
```

#### 代码

```java
class Solution {
    public int numDecodings(String s) {
        int n=s.length();
        int[] dp=new int[n+1];
        dp[n]=1;
        for(int i=n-1;i>=0;i--) {
            if(s.charAt(i)!='0') {
                dp[i]=dp[i+1];
                if(i<n-1&&(s.charAt(i)=='1'||s.charAt(i)=='2'&&s.charAt(i+1)<'7')) {
                    dp[i]+=dp[i+2];
                }
            }
        }
        return dp[0];
    }
}
```

