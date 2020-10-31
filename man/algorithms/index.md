# Algorithms

## Sudoku

1) We have a pull of sudoku numbers.
2) Create three groups of pools.
3) Pull for 1 horizontal line.
4) Pull for 9 vertical lines.
5) Pull for 9 squares 3x3.
6) For each cell, check if sudoku numbers have already been used in the pools related to this cell? 
We check the horizontal pool, one vertical pool and one square 3x3 pool. 
If used, then remove this value from our pool of sudoku numbers.
7) If there are no numbers left in the pool of sudoku numbers, then we need to erase the entire line, clear the related pools and recreate the line.
8) If attempts to rearrange the numbers do not help (usually this is the 6th line), then we are trying to recreate the entire table.
9) If there are numbers in the pool of sudoku numbers, then we take a random number from these numbers and put it in the table.
10) We also add the selected used number to three pools: a horizontal pool, one vertical pool and one square pool.
