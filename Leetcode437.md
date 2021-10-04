---
title: Leetcode 437. Path Sum III 路径总和 III
author: Mark
summary: 使用递归，遍历二叉树节点，并递归以此节点为根的二叉树，统计路径和
tags:
  - leetcode
  - algorithm
  - recursion
categories:
  - 算法
abbrlink: 7e0676ea
date: 2021-09-27 14:13:00
---

Given the `root` of a binary tree and an integer `targetSum`, return *the number of paths where the sum of the values along the path equals* `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

 

**Example 1:**

![img](https://cdn.jsdelivr.net/gh/cumark/picBed/pathsum3-1-tree.jpg)

```
Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.
```

**Example 2:**

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: 3
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 1000]`.
- `-109 <= Node.val <= 109`
- `-1000 <= targetSum <= 1000`





## 分析

针对二叉树相关的问题，优先考虑递归，可以设置两个函数，主函数和统计路径数量的遍历函数

主函数：遍历所有节点，传递节点给遍历函数

遍历函数：得到节点后，以节点为根节点，累加路径的数量

#### 方法

使用递归，遍历二叉树节点，并递归以此节点为根的二叉树，统计路径和

#### 代码

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int pathSum(TreeNode root, int targetSum) {
        if(root==null) return 0;
        return traverse(root,targetSum)+pathSum(root.left,targetSum)+pathSum(root.right,targetSum);
    }
    public int traverse(TreeNode node,int sum) {
        if(node==null) return 0;
        return (sum==node.val?1:0)+traverse(node.left,sum-node.val)+traverse(node.right,sum-node.val);
    }
}
```

