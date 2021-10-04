---
title: Leetcode 430. Flatten a Multilevel Doubly Linked List 扁平化多级双向链表
author: Mark
summary: 给出一个多级双向链表，要求将其扁平化，也就是将多级转变为单极，这种形式与二叉树链表的先序遍历非常相似，因此优先考虑深度优先搜索遍历
tags:
  - leetcode
  - algorithm
  - dfs
categories:
  - 算法
abbrlink: 345fb18b
date: 2021-09-24 11:02:00
---

You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.



**Example 1:**

```
Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
Output: [1,2,3,7,8,11,12,9,10,4,5,6]
Explanation
The multilevel linked list in the input is as follows:
```

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928211328.png)

After flattening the multilevel linked list it becomes:

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928211346.png)

**Example 2:**

```
Input: head = [1,2,null,3]
Output: [1,3,2]
Explanation:

The input multilevel linked list is as follows:

  1---2---NULL
  |
  3---NULL
```

**Example 3:**

```
Input: head = []
Output: []
```

 

**How multilevel linked list is represented in test case:**

We use the multilevel linked list from **Example 1** above:

```
 1---2---3---4---5---6--NULL
         |
         7---8---9---10--NULL
             |
             11--12--NULL
```

The serialization of each level is as follows:

```
[1,2,3,4,5,6,null]
[7,8,9,10,null]
[11,12,null]
```

To serialize all levels together we will add nulls in each level to signify no node connects to the upper node of the previous level. The serialization becomes:

```
[1,2,3,4,5,6,null]
[null,null,7,8,9,10,null]
[null,11,12,null]
```

Merging the serialization of each level and removing trailing nulls we obtain:

```
[1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
```

 

**Constraints:**

- The number of Nodes will not exceed `1000`.
- `1 <= Node.val <= 10^5`

分析：这道题给出一个多级双向链表，要求将其扁平化，也就是将多级转变为单极，这种形式与二叉树链表的先序遍历非常相似，因此优先考虑深度优先搜索遍历



## 方法

从head开始遍历链表，当遇到存在child节点时，则保存node.next，然后dfs node.child（与二叉树先序优先搜索遍历相似），将node.next与node.child构建先后续关系，node.child置于null。dfs最终得到child节点的尾节点，将尾节点和之前保存的node.next构建先后续关系，dfs深层遍历后回溯到之前的层，把每一层child节点的前后构建完成。

#### 代码

```java
*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
};
*/

class Solution {
    public Node flatten(Node head) {
        dfs(head);
        return head;
    }
    public Node dfs(Node node) {
        Node cur=node;
        Node last=null;
        while(cur!=null) {
            Node next=cur.next;
            if(cur.child!=null) {
                Node childLast=dfs(cur.child);
                next=cur.next;
                cur.next=cur.child;
                cur.child.prev=cur;
                if(next!=null) {
                    childLast.next=next;
                    next.prev=childLast;
                }
                cur.child=null;
                last=childLast;
            } else {
                last=cur;
            }
            cur=next;
        }
        return last;
    }
}
```

