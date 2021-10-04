---
title: Leetcode 151. Reverse Words in a String 翻转字符串里的单词
author: Mark
summary: 应用java本身的特性，消除string前后空格以及单词之间的空格，反转单词，再转化为string即可
tags:
  - leetcode
  - algorithm
categories:
  - 算法
  - java
abbrlink: a17663d9
date: 2021-09-27 20:05:00
---

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space.*

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

**Example 1:**

```
Input: s = "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

**Example 4:**

```
Input: s = "  Bob    Loves  Alice   "
Output: "Alice Loves Bob"
```

**Example 5:**

```
Input: s = "Alice does not even like bob"
Output: "bob like even not does Alice"
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is **at least one** word in `s`.

 

**Follow-up:** If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?



## 分析

1.String中前后可能有空格，可以使用s.trim()方法消除

2.单词前后可能有多个空格，可以使用s.split(" +")方法消除，其中空格表示间隔的字符，+表示一个及超过一个字符

3.需要反转单词顺序，应用Collections.reverse(list)的方法，将数组用Arrays.asList（）方法转化为list

4.当前已经求出一个已反转的list，可以应用String.join(" ",list/array)的方法，在单词见加入空格并汇集成string

#### 方法

应用java本身的特性，消除string前后空格以及单词之间的空格，反转单词，再转化为string即可

#### 代码

```java
public String reverseWords(String s) {
    String[] words = s.trim().split(" +");
    Collections.reverse(Arrays.asList(words));
    return String.join(" ", words);
}
```

