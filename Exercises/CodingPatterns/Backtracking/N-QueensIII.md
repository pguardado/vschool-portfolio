## Problem Summary

The problem is to place \( n \) queens on an \( n \times n \) chessboard such that no two queens attack each other.

## Logic to Solve

The solution involves backtracking to explore all possible configurations of placing the queens on the chessboard. The approach can be summarized as follows:

1. Initialize an empty chessboard of size \( n \times n \).
2. Use a recursive backtracking function to explore all possible configurations.
3. At each step, try placing a queen in a row such that it does not conflict with the queens already placed on the board.
4. If a queen can be placed in a row without conflicts, recursively explore further by placing queens in the subsequent rows.
5. If a valid configuration is found (all queens are placed), add it to the result list.
6. Continue exploring all possible configurations recursively.
7. Finally, return the list of valid configurations.

## Step-by-Step Analysis

1. **Initialization**:
   - Initialize an empty array to store the valid configurations.
2. **Backtracking**:
   - Use a recursive backtracking function to explore all possible configurations.
   - At each step, try placing a queen in a row such that it does not conflict with the queens already placed on the board.
   - If a queen can be placed in a row without conflicts, recursively explore further by placing queens in the subsequent rows.
   - If a valid configuration is found (all queens are placed), add it to the result list.
3. **Base Case**:
   - If all queens are placed on the board, add the current configuration to the result list.
4. **Result**:
   - The result list contains all valid configurations.

## Pseudocode

```
function solveNQueens(n):
    result = []

    function isSafe(board, row, col):
        // Check if there is no queen in the same column or diagonals
        for i from 0 to row - 1:
            if board[i][col] === 'Q':
                return false
            if col - (row - i) >= 0 && board[i][col - (row - i)] === 'Q':
                return false
            if col + (row - i) < n && board[i][col + (row - i)] === 'Q':
                return false
        return true

    function backtrack(board, row):
        if row === n:
            result.push(board.slice())
            return

        for col from 0 to n - 1:
            if isSafe(board, row, col):
                board[row][col] = 'Q'
                backtrack(board, row + 1)
                board[row][col] = '.'

    emptyBoard = Array(n).fill().map(() => Array(n).fill('.'))
    backtrack(emptyBoard, 0)
    return result
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function solveNQueens(n) {
  const result = [];

  function isSafe(board, row, col) {
    // Check if there is no queen in the same column or diagonals
    for (let i = 0; i < row; i++) {
      if (board[i][col] === "Q") {
        return false;
      }
      if (col - (row - i) >= 0 && board[i][col - (row - i)] === "Q") {
        return false;
      }
      if (col + (row - i) < n && board[i][col + (row - i)] === "Q") {
        return false;
      }
    }
    return true;
  }

  function backtrack(board, row) {
    if (row === n) {
      result.push(board.map((row) => row.join("")));
      return;
    }

    for (let col = 0; col < n; col++) {
      if (isSafe(board, row, col)) {
        board[row][col] = "Q";
        backtrack(board, row + 1);
        board[row][col] = ".";
      }
    }
  }

  const emptyBoard = Array(n)
    .fill()
    .map(() => Array(n).fill("."));
  backtrack(emptyBoard, 0);
  return result;
}

// Example usage:
console.log(solveNQueens(4)); // Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
```

### Explanation

- The `solveNQueens` function initializes an empty array `result` to store the valid configurations.
- It defines a nested `isSafe` function to check if it's safe to place a queen in a particular position on the chessboard.
- The `isSafe` function takes parameters `board`, `row`, and `col`, representing the current state of the chessboard and the position to check, respectively.
- It checks if there are no queens in the same column or diagonals of the current position.
- The `backtrack` function is used to recursively explore all possible configurations of placing queens on the chessboard.
- It takes parameters `board` and `row`, representing the current state of the chessboard and the current row being explored, respectively.
- At each step, it tries placing a queen in a column of the current row if it's safe to do so.
- If a valid configuration is found (all queens are placed), it adds it to the result list.
- Finally, it returns the list of valid configurations.
