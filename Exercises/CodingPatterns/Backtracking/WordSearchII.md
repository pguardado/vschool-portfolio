## Problem Summary

The problem is to find all words from a given list that can be formed by traversing adjacent cells on an `m x n` board of characters. Two cells are considered adjacent if they share an edge. The words can be formed by traversing horizontally or vertically, but not diagonally. Each cell on the board can be used only once in a word.

## Logic to Solve

The solution involves using a Trie data structure to efficiently search for words in the board. The approach can be summarized as follows:

1. Construct a Trie from the given list of words.
2. Traverse the board and for each cell, perform a depth-first search (DFS) to search for words starting from that cell.
3. During the DFS, use backtracking to explore all possible paths and check if the current path forms a valid word according to the Trie.
4. If a valid word is found, add it to the result list.

## Step-by-Step Analysis

1. **Trie Construction**:
   - Build a Trie from the list of words to efficiently search for words during traversal.
2. **DFS Traversal**:
   - For each cell in the board, perform a DFS to search for words starting from that cell.
   - During the DFS, maintain a current word being formed by traversing cells.
   - Use backtracking to explore all possible paths from the current cell.
   - If the current word forms a valid word according to the Trie, add it to the result list.
3. **Backtracking**:
   - During the DFS, mark visited cells to avoid revisiting them in the same path.
   - After exploring a path, unmark the cell to backtrack and explore other paths.

## Pseudocode

```
function findWords(board, words):
    result = []

    function buildTrie(words):
        trie = {}
        for word in words:
            node = trie
            for char in word:
                if char not in node:
                    node[char] = {}
                node = node[char]
            node['$'] = word
        return trie

    trie = buildTrie(words)

    function dfs(row, col, node):
        char = board[row][col]
        if char not in node:
            return

        curr_word = node[char].pop('$', None)
        if curr_word:
            result.append(curr_word)

        board[row][col] = '#'  # mark as visited

        for dr, dc in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
            nr, nc = row + dr, col + dc
            if 0 <= nr < len(board) and 0 <= nc < len(board[0]) and board[nr][nc] != '#':
                dfs(nr, nc, node[char])

        board[row][col] = char  # backtrack

    for i in range(len(board)):
        for j in range(len(board[0])):
            dfs(i, j, trie)

    return result
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function findWords(board, words) {
  const result = [];

  function buildTrie(words) {
    const trie = {};
    for (const word of words) {
      let node = trie;
      for (const char of word) {
        if (!node[char]) {
          node[char] = {};
        }
        node = node[char];
      }
      node["$"] = word;
    }
    return trie;
  }

  const trie = buildTrie(words);

  function dfs(row, col, node) {
    const char = board[row][col];
    if (!node[char]) return;

    const currWord = node[char]["$"];
    if (currWord) {
      result.push(currWord);
      delete node[char]["$"];
    }

    board[row][col] = "#"; // mark as visited

    const directions = [
      [1, 0],
      [-1, 0],
      [0, 1],
      [0, -1],
    ];
    for (const [dr, dc] of directions) {
      const nr = row + dr;
      const nc = col + dc;
      if (
        nr >= 0 &&
        nr < board.length &&
        nc >= 0 &&
        nc < board[0].length &&
        board[nr][nc] !== "#"
      ) {
        dfs(nr, nc, node[char]);
      }
    }

    board[row][col] = char; // backtrack
  }

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[0].length; j++) {
      dfs(i, j, trie);
    }
  }

  return result;
}

// Example usage:
const board = [
  ["o", "a", "a", "n"],
  ["e", "t", "a", "e"],
  ["i", "h", "k", "r"],
  ["i", "f", "l", "v"],
];
const words = ["oath", "pea", "eat", "rain"];
console.log(findWords(board, words)); // Output: ["eat", "oath"]
```

### Explanation

- The `findWords` function initializes an empty array `result` to store the found words.
- It constructs a Trie from the given list of words to efficiently search for words during traversal.
- The `dfs` function performs a depth-first search (DFS) on the board:
  - It traverses the board starting from the current cell `(row, col)` and searches for words in the Trie.
  - If a word is found in the Trie, it is added to the result list, and the corresponding entry is removed from the Trie to avoid duplicate entries.
  - During the DFS, cells are marked as visited to avoid revisiting them in the same path.
  - After exploring a path, cells are unmarked to backtrack and explore other paths.
- The main loop iterates over each cell in the
