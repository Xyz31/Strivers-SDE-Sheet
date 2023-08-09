# 	Sudoko Solver


Sample Input 1:
1
9 0 0 0 2 0 7 5 0 
6 0 0 0 5 0 0 4 0 
0 2 0 4 0 0 0 1 0 
2 0 8 0 0 0 0 0 0 
0 7 0 5 0 9 0 6 0 
0 0 0 0 0 0 4 0 1 
0 1 0 0 0 5 0 8 0 
0 9 0 0 7 0 0 0 4 
0 8 2 0 4 0 0 0 6


Sample Output 1:
yes


Explanation Of The Sample Input1:
One of the possible solutions is:
9 4 1 3 2 6 7 5 8
6 3 7 1 5 8 2 4 9
8 2 5 4 9 7 6 1 3
2 6 8 7 1 4 3 9 5
1 7 4 5 3 9 8 6 2
3 5 9 6 8 2 4 7 1
4 1 3 2 6 5 9 8 7
5 9 6 8 7 3 1 2 4
7 8 2 9 4 1 5 3 6

## code
```cpp

// Check if a number is valid to be placed at a specific position in the Sudoku board
bool isValid(int board[9][9], int row, int col, int num) {
  // Check row
  for (int i = 0; i < 9; i++) {
    if (board[row][i] == num)
      return false;
  }

  // Check column
  for (int i = 0; i < 9; i++) {
    if (board[i][col] == num)
      return false;
  }

  // Check 3x3 box
  int boxStartRow = 3 * (row / 3);
  int boxStartCol = 3 * (col / 3);
  for (int i = boxStartRow; i < boxStartRow + 3; i++) {
    for (int j = boxStartCol; j < boxStartCol + 3; j++) {
      if (board[i][j] == num)
        return false;
    }
  }

  return true;
}

// Recursive function to solve the Sudoku puzzle
bool solveSudoku(int board[9][9]) {
  for (int row = 0; row < 9; row++) {
    for (int col = 0; col < 9; col++) {
      if (board[row][col] == 0) {  // Empty cell, need to fill
        for (int num = 1; num <= 9; num++) {
          if (isValid(board, row, col, num)) {  // Check if the number is valid
            board[row][col] = num;  // Place the number

            if (solveSudoku(board))  // Recursively solve the rest of the puzzle
              return true;
            else
              board[row][col] = 0;  // Undo the choice and try a different number
          }
        }
        return false;  // No valid number found for this cell, backtrack
      }
    }
  }
  return true;  // Sudoku solved, all cells filled
}

// Function to check if the given Sudoku board can be solved
bool isItSudoku(int board[9][9]) {
  return solveSudoku(board);
}

```