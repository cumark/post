---
title: "Leetcode 725. Split Linked List in Parts 分隔链表"
author: Mark
summary: 使用两个for循环，把被分割的每一段链表的开端设为上一段的next，流畅实现链表分隔
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: b75f9389
date: 2021-09-22 14:34:00
---
---

Given the `head` of a singly linked list and an integer `k`, split the linked list into `k` consecutive linked list parts.

The length of each part should be as equal as possible: no two parts should have a size differing by more than one. This may lead to some parts being null.

The parts should be in the order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal to parts occurring later.

Return *an array of the* `k` *parts*.

 

**Example 1:**

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928212303.png)

```
Input: head = [1,2,3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but its string representation as a ListNode is [].
```

**Example 2:**

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928212320.png)

```
Input: head = [1,2,3,4,5,6,7,8,9,10], k = 3
Output: [[1,2,3,4],[5,6,7],[8,9,10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
```

 

**Constraints:**

- The number of nodes in the list is in the range `[0, 1000]`.
- `0 <= Node.val <= 1000`
- `1 <= k <= 50`

## 分析

这道题要把一个ListNode链表，平均分隔为k段，有部分数量可能多一个，放到前面。对于一道 Medium 题而言，思路比较清晰，主要就是考察了一个对链表的使用和对细节的把握，可以使用两个for循环，把被分割的每一段链表的开端设为上一段的next，

```java
res[i]=cur;
int part=every+(suff>i?1:0);
```

对于每一段链表的结尾，则采用如下方式，让末尾的后置设为null

```java
ListNode next=cur.next;
cur.next=null;
cur=next;
```

然后比较这个距离和，跟总距离减去该距离所得结果之间的较小值返回即可

#### 代码：

```java
class Solution {
    public ListNode[] splitListToParts(ListNode head, int k) {
        int sum=0;
        ListNode cur=head;
        while(head!=null) {
            sum++;
            head=head.next;
        }
        int suff=sum%k;int every=sum/k;
        ListNode[] res=new ListNode[k];
        for(int i=0;i<k&&cur!=null;i++) {
            res[i]=cur;
            int part=every+(suff>i?1:0);
            for(int j=1;j<part;j++) {
                cur=cur.next;
            }
            ListNode next=cur.next;
            cur.next=null;
            cur=next;
        }
        return res;
    }
}
```

