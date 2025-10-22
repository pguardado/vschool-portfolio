## Problem Summary

The Sudoku Solver problem involves solving a given 9x9 Sudoku board by filling in the empty cells (denoted by '.') such that each row, each column, and each of the nine 3x3 sub-grids contain all of the digits from 1 to 9 exactly once.

## Logic to Solve

The solution involves using backtracking to try placing digits in empty cells and recursively attempting to solve the board. The approach can be summarized as follows:

1. Find an empty cell.
2. Attempt to place each digit from 1 to 9 in the empty cell.
3. Check if placing the digit is valid (i.e., it does not violate Sudoku rules).
4. If the digit is valid, place it and recursively attempt to solve the rest of the board.
5. If placing the digit leads to a solution, return true. Otherwise, backtrack by removing the digit and trying the next digit.
6. If no digit can be placed in the current empty cell, return false.

## Step-by-Step Analysis

1. **Validation**:
   - Create a function to check if placing a digit in a given cell is valid.
2. **Find Empty Cell**:
   - Create a function to find the next empty cell on the board.
3. **Backtracking**:
   - Use a recursive function to solve the board by placing digits and backtracking if necessary.

## Pseudocode

```
function solveSudoku(board):
    function isValid(board, row, col, num):
        for i in range(9):
            if board[row][i] == num or board[i][col] == num:
                return False
            if board[row - row % 3 + i // 3][col - col % 3 + i % 3] == num:
                return False
        return True

    function solve(board):
        for row in range(9):
            for col in range(9):
                if board[row][col] == '.':
                    for num in '123456789':
                        if isValid(board, row, col, num):
                            board[row][col] = num
                            if solve(board):
                                return True
                            board[row][col] = '.'
                    return False
        return True

    solve(board)
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function solveSudoku(board) {
  function isValid(board, row, col, num) {
    for (let i = 0; i < 9; i++) {
      if (board[row][i] === num || board[i][col] === num) {
        return false;
      }
      const boxRow = 3 * Math.floor(row / 3) + Math.floor(i / 3);
      const boxCol = 3 * Math.floor(col / 3) + (i % 3);
      if (board[boxRow][boxCol] === num) {
        return false;
      }
    }
    return true;
  }

  function solve(board) {
    for (let row = 0; row < 9; row++) {
      for (let col = 0; col < 9; col++) {
        if (board[row][col] === ".") {
          for (let num = "1"; num <= "9"; num++) {
            if (isValid(board, row, col, num)) {
              board[row][col] = num;
              if (solve(board)) {
                return true;
              }
              board[row][col] = ".";
            }
          }
          return false;
        }
      }
    }
    return true;
  }

  solve(board);
}

// Example usage:
let board = [
  ["5", "3", ".", ".", "7", ".", ".", ".", "."],
  ["6", ".", ".", "1", "9", "5", ".", ".", "."],
  [".", "9", "8", ".", ".", ".", ".", "6", "."],
  ["8", ".", ".", ".", "6", ".", ".", ".", "3"],
  ["4", ".", ".", "8", ".", "3", ".", ".", "1"],
  ["7", ".", ".", ".", "2", ".", ".", ".", "6"],
  [".", "6", ".", ".", ".", ".", "2", "8", "."],
  [".", ".", ".", "4", "1", "9", ".", ".", "5"],
  [".", ".", ".", ".", "8", ".", ".", "7", "9"],
];

solveSudoku(board);
console.log(board);
```

### Explanation

- The `solveSudoku` function initiates the solving process by defining two helper functions: `isValid` and `solve`.
- The `isValid` function checks if placing a digit in a given cell is valid by ensuring that the digit is not already present in the same row, column, or 3x3 sub-grid.
- The `solve` function attempts to fill the board by iterating over each cell:
  - If an empty cell is found (denoted by `'.'`), it tries placing each digit from '1' to '9' in the cell.
  - If placing a digit is valid, it places the digit and recursively attempts to solve the rest of the board.
  - If the recursive call returns true, the board is solved.
  - If no digit leads to a solution, it backtracks by resetting the cell to `'.'` and trying the next digit.
- The initial call to `solve` starts the backtracking process. Once the board is solved, the modified board is printed.
