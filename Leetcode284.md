---
title: Leetcode 284. Peeking Iterator 顶端迭代器
author: Mark
summary: 利用iterator的类，实现题目所定义的要求
tags:
  - leetcode
  - algorithm
  - design
categories:
  - 算法
date: 2021-10-11 21:47:00
---

Design an iterator that supports the peek operation on a list in addition to the hasNext and the next operations.

Implement the PeekingIterator class:

+ PeekingIterator(int[] nums) Initializes the object with the given integer array nums.
+ int next() Returns the next element in the array and moves the pointer to the next element.
+ bool hasNext() Returns true if there are still elements in the array.
+ int peek() Returns the next element in the array without moving the pointer.
 

Example 1:

```
Input
["PeekingIterator", "next", "peek", "next", "next", "hasNext"]
[[[1, 2, 3]], [], [], [], [], []]
Output
[null, 1, 2, 2, 3, false]

Explanation
PeekingIterator peekingIterator = new PeekingIterator([1, 2, 3]); // [1,2,3]
peekingIterator.next();    // return 1, the pointer moves to the next element [1,2,3].
peekingIterator.peek();    // return 2, the pointer does not move [1,2,3].
peekingIterator.next();    // return 2, the pointer moves to the next element [1,2,3]
peekingIterator.next();    // return 3, the pointer moves to the next element [1,2,3]
peekingIterator.hasNext(); // return False
``` 


Constraints:

+ 1 <= nums.length <= 1000
+ 1 <= nums[i] <= 1000
+ All the calls to next and peek are valid.
+ At most 1000 calls will be made to next, hasNext, and peek.
 

Follow up: How would you extend your design to be generic and work with all types, not just integer?


## 分析

这道题主要是利用iterator的类，实现题目所定义的要求，个人感觉这类题目没太高的难度，也不必把问题想得过于复杂，独栋题意，简单实现功能即可。

#### 方法

+ 定义Iterator类，使用，Iterator<T> iter=iterator来定义
+ 使用next指标指着下一个元素
+ 在peek函数中，显示next指标
+ 在next（）函数中，首先要实现peek函数相同的功能，即显示next指标，另外还要让next转移到下一个元素，
    使用next = iter.hasNext() ? iter.next() : null来实现


#### 代码

```java
class PeekingIterator implements Iterator<Integer> {
    private Integer next = null;
    private Iterator<Integer> iter;

    public PeekingIterator(Iterator<Integer> iterator) {
        // initialize any member here.
        iter = iterator;
        if (iter.hasNext())
            next = iter.next();
    }
    
    // Returns the next element in the iteration without advancing the iterator. 
    public Integer peek() {
        return next; 
    }

    // hasNext() and next() should behave the same as in the Iterator interface.
    // Override them if needed.
    @Override
    public Integer next() {
        Integer res = next;
        next = iter.hasNext() ? iter.next() : null;
        return res; 
    }

    @Override
    public boolean hasNext() {
        return next != null;
    }
}
```

