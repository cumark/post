---
title: Leetcode 273. Integer to English Words 整数转换英文表示
author: Mark
summary: 使用String数组分别储存，小于20，十的倍数，和千以上的三个单位，对于大于千的单位，在千之前加上取余的变化，对大于千的数量，从后往前遍历
tags:
  - leetcode
  - algorithm
categories:
  - 算法
date: 2021-10-12 14:32:00
---
Convert a non-negative integer num to its English words representation.

 

Example 1:

```
Input: num = 123
Output: "One Hundred Twenty Three"
```
Example 2:

```
Input: num = 12345
Output: "Twelve Thousand Three Hundred Forty Five"
```
Example 3:

```
Input: num = 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```
Example 4:

```
Input: num = 1234567891
Output: "One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```
 

Constraints:

+ 0 <= num <= 2^31 - 1



## 分析

1.这是一个有趣的问题，将数字转换为用英文表示，英文的计数，从上到下，为Billion，Million，Thousand，Hundred等，可以从上到下进行递归

2.对于大于Thousand的单位，按照十进制，从后往前，每三位为标准进行遍历

3.对于小于Thousand的单位，从小于20，小于100，大于100三个层次进行以此判别，这个步骤也要应用于大于Thousand的单位之前

#### 方法

使用String数组分别储存，小于20，十的倍数，和千以上的三个单位，对于大于千的单位，在千之前加上取余的变化，对大于千的数量，从后往前遍历


#### 代码

```java
class Solution {
    String[] less={"","One","Two","Three","Four","Five","Six","Seven","Eight","Nine","Ten","Eleven","Twelve","Thirteen","Fourteen","Fifteen","Sixteen","Seventeen","Eighteen","Nineteen"};
    String[] tens={"","Ten","Twenty","Thirty","Forty","Fifty","Sixty","Seventy","Eighty","Ninety"};
    String[] thousands={"","Thousand","Million","Billion"};
    public String numberToWords(int num) {
        if(num==0) return "Zero";
        int i=0;
        String words="";
        while(num>0) {
            if(num%1000!=0) {
                words=helper(num%1000)+thousands[i]+" "+words;
            }
            num/=1000;
            i++;
            }
            return words.trim();
        }
        public String helper(int num) {
            if(num==0) {
                return "";
            } else if(num<20) {
                return less[num]+" ";
            } else if(num<100) {
                return tens[num/10]+" "+helper(num%10);
            } else {
                return less[num/100]+" Hundred "+helper(num%100);
            }
        }
}
```

