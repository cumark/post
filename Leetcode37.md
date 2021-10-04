---
title: Leetcode 37. Sudoku Solver 解数独
author: Mark
summary: >-
  采用递归回溯法，分为主函数和回溯函数和验证函数，主函数：传递到回溯函数，回溯函数：遍历数组数独，递归验证是否符合数独标准，若不符合则回溯至上一层，直到全部符合数独标准为止，验证函数：只验证新改变的坐标是否符合数独
tags:
  - leetcode
  - algorithm
  - dfs
  - backtrace
categories:
  - 算法
abbrlink: a7061b21
date: 2021-09-28 14:13:00
---

- Write a program to solve a Sudoku puzzle by filling the empty cells.

  A sudoku solution must satisfy **all of the following rules**:

  1. Each of the digits `1-9` must occur exactly once in each row.
  2. Each of the digits `1-9` must occur exactly once in each column.
  3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

  The `'.'` character indicates empty cells.

   

  **Example 1:**

  ![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928141109.png)

  ```
  Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
  Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
  Explanation: The input board is shown above and the only valid solution is shown below:
  ```

   ![](https://cdn.jsdelivr.net/gh/cumark/picBed/20210928141144.png)

  **Constraints:**

  - `board.length == 9`
  - `board[i].length == 9`
  - `board[i][j]` is a digit or `'.'`.
  - It is **guaranteed** that the input board has only one solution.





## 分析

这道题要求解`9*9`数组数独，可以采用递归回溯法，分为主函数和回溯函数和验证函数，

主函数：传递到回溯函数

回溯函数：遍历数组数独，递归验证是否符合数独标准，若不符合则回溯至上一层，直到全部符合数独标准为止。

验证函数：只验证新改变的坐标是否符合数独

#### 方法

使用递归回溯的方法，不断验证，直到出现符合全部数独标准的一组结果。

#### 代码

```java
class Solution {
    public void solveSudoku(char[][] board) {
        solve(board);
    }
    public boolean solve(char[][] board) {
        for(int i=0;i<board.length;i++) {
            for(int j=0;j<board[0].length;j++) {
                if(board[i][j]=='.') {
                    for(char ch='1';ch<='9';ch++) {
                        if(isValid(board,i,j,ch)) {
                            board[i][j]=ch;
                            if(solve(board)) {
                                return true;
                            } else {
                                board[i][j]='.';
                            }
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    public boolean isValid(char[][] board,int i,int j,char ch) {
        for(int index=0;index<9;index++) {
            if(board[index][j]!='.'&&board[index][j]==ch) return false;
            if(board[i][index]!='.'&&board[i][index]==ch) return false;
            if(board[3*(i/3)+index/3][3*(j/3)+index%3]!='.'&&board[3*(i/3)+index/3][3*(j/3)+index%3]==ch) return false;
        }
        return true;
    }
}
```

