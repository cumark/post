---
title: Leetcode 130. Surrounded Regions 被围绕的区域
author: Mark
summary: 仅dfs遍历矩阵的边缘，对于O，则进行dfs遍历，并将之置为M。最后再将所有M置为O，O置为X即可。
tags:
  - leetcode
  - algorithm
  - dfs
categories:
  - 算法
abbrlink: 372ac7d5
date: 2021-09-28 13:42:00
---

Given an `m x n` matrix `board` containing `'X'` and `'O'`, *capture all regions that are 4-directionally surrounded by* `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

 

**Example 1:**

![img](https://cdn.jsdelivr.net/gh/cumark/picBed/xogrid.jpg)

```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```

**Example 2:**

```
Input: board = [["X"]]
Output: [["X"]]
```

 

**Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is `'X'` or `'O'`.





## 分析

这道题要求边缘O及与边缘的O直接相连的O不做改变，其他的O全部改为X，那么可以仅dfs遍历矩阵的边缘，对于O，则进行dfs遍历，并将之置为M。最后再将所有M置为O，O置为X即可。



#### 方法

采用dfs，遍历矩阵边缘，最后再遍历整个矩阵，将所作的标记更新

#### 代码

```java
class Solution {
    public void solve(char[][] board) {
        if(board.length<1||board[0].length<1) {
            return ;
        }
        for(int i=0;i<board.length;i++) {
            dfs(board,i,0);
            dfs(board,i,board[0].length-1);
        }
        for(int i=0;i<board[0].length;i++) {
            dfs(board,0,i);
            dfs(board,board.length-1,i);
        }
        for(int i=0;i<board.length;i++) {
            for(int j=0;j<board[0].length;j++) {
                if(board[i][j]=='M') {
                    board[i][j]='O';
                } else {
                    board[i][j]='X';
                }
            }
        }
    }
    public void dfs(char[][] board,int i,int j) {
        if(i<0||i>=board.length||j<0||j>=board[0].length||board[i][j]!='O') {
            return ;
        }
            board[i][j]='M';
            dfs(board,i+1,j);
            dfs(board,i,j+1);
            dfs(board,i-1,j);
            dfs(board,i,j-1);
    }
}
```

