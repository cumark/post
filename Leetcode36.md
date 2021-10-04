---
title: Leetcode 36. Valid Sudoku 有效的数独
author: Mark
summary: '难点在于对9宫格之中`3*3`方格的验证，这里可以采用`board[(i/3)*3+j/3][(i%3)*3+j%3]`的方式进行表示，遍历即可'
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: 5cf1e14c
date: 2021-09-28 14:00:00
---

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

 

**Example 1:**

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928140252.png)

```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**

```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

 

**Constraints:**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.





## 分析

这道题要求验证当前状态下的`9*9`数组是否为有效的数独，难点在于对9宫格之中`3*3`方格的验证，这里可以采用`board[(i/3)*3+j/3][(i%3)*3+j%3]`的方式进行表示，遍历即可



#### 方法

遍历9*9数组，若不出现重复，则返回true

#### 代码

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        for(int i=0;i<9;i++) {
            Set<Character> set=new HashSet();
            for(int j=0;j<9;j++) {
                if(!set.contains(board[i][j])&&board[i][j]!='.') {
                    set.add(board[i][j]);
                } else if(board[i][j]!='.'){
                    return false;
                }
            }
            set=new HashSet();
            for(int j=0;j<9;j++) {
                if(!set.contains(board[j][i])&&board[j][i]!='.') {
                    set.add(board[j][i]);
                } else if(board[j][i]!='.'){
                    return false;
                }
            }
            set=new HashSet();
            for(int j=0;j<9;j++) {
                if(!set.contains(board[(i/3)*3+j/3][(i%3)*3+j%3])&&board[(i/3)*3+j/3][(i%3)*3+j%3]!='.')     { 
                    set.add(board[(i/3)*3+j/3][(i%3)*3+j%3]);
                } else if(board[(i/3)*3+j/3][(i%3)*3+j%3]!='.'){
                    return false;
                }
            }
        }
        return true;
    }
}
```

