## Problem Summary

The N-Queens problem involves placing `n` queens on an `n x `n` chessboard such that no two queens can attack each other. This means no two queens can be in the same row, column, or diagonal.

## Logic to Solve

The solution involves using backtracking to explore all possible placements of queens on the board. The approach can be summarized as follows:

1. Use a recursive function to place queens row by row.
2. For each row, attempt to place a queen in each column and check if it is a valid placement (i.e., it is not attacked by any previously placed queens).
3. If a valid placement is found, place the queen and recursively attempt to place queens in the next row.
4. Backtrack by removing the queen and trying the next column.

## Step-by-Step Analysis

1. **Initialization**:
   - Use an empty list to store the solutions.
   - Represent the board as a list of integers where the index represents the row and the value represents the column of the queen.
2. **Validation**:
   - Create a function to check if placing a queen at a given position is valid (i.e., it does not conflict with any previously placed queens).
3. **Recursion/Base Case**:
   - If all queens are placed (i.e., the current row equals `n`), add the current board configuration to the results.
   - For each column in the current row, check if placing a queen there is valid.
   - If valid, place the queen and recursively attempt to place queens in the next row.
4. **Backtracking**:
   - After exploring a placement, remove the queen and try the next column.

## Pseudocode

```
function solveNQueens(n):
    results = []

    function isValid(board, row, col):
        for r in range(row):
            if board[r] == col or abs(board[r] - col) == abs(r - row):
                return False
        return True

    function backtrack(row, board):
        if row == n:
            results.append(boardToString(board))
            return

        for col in range(n):
            if isValid(board, row, col):
                board[row] = col
                backtrack(row + 1, board)
                board[row] = -1  # backtrack

    function boardToString(board):
        return [''.join(['Q' if board[r] == c else '.' for c in range(n)]) for r in range(n)]

    backtrack(0, [-1] * n)
    return results
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function solveNQueens(n) {
  const results = [];

  function isValid(board, row, col) {
    for (let r = 0; r < row; r++) {
      if (board[r] === col || Math.abs(board[r] - col) === Math.abs(r - row)) {
        return false;
      }
    }
    return true;
  }

  function backtrack(row, board) {
    if (row === n) {
      results.push(boardToString(board));
      return;
    }

    for (let col = 0; col < n; col++) {
      if (isValid(board, row, col)) {
        board[row] = col;
        backtrack(row + 1, board);
        board[row] = -1; // backtrack
      }
    }
  }

  function boardToString(board) {
    return board.map((r) => {
      let rowStr = new Array(n).fill(".");
      rowStr[r] = "Q";
      return rowStr.join("");
    });
  }

  backtrack(0, new Array(n).fill(-1));
  return results;
}

// Example usage:
console.log(solveNQueens(4));
```

### Explanation

- The `solveNQueens` function initializes an empty array `results` to store the board configurations.
- The `isValid` function checks if placing a queen at the specified `row` and `col` is valid by ensuring it does not conflict with any previously placed queens.
- The `backtrack` function attempts to place queens starting from the given `row`.
  - If all queens are placed (i.e., `row === n`), a string representation of the board is added to `results`.
  - For each column in the current row, it checks if placing a queen there is valid.
  - If valid, the queen is placed, and `backtrack` is called recursively for the next row.
  - After the recursive call, the queen is removed to backtrack and try the next column.
- The `boardToString` function converts the board representation into the required format of strings.
- The initial call to `backtrack` starts with `row` equal to 0 and an empty board. The function returns `results` after all valid configurations are generated.
