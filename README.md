# BINGO
Least average tries to open a bingo line

There's a n\times n bingo board, one of the n columns, n rows and 2 diagonals contains prizes, what's the best strategy to open all cells of that line? Assuming an equal chance of every 2n+2 line being the bingo one it goes as follows.

A strategy works as follows: you check a spot s_i, if it has the prize you check its neighboors, if it's empty you proceed to s_(i+1)
The average number of opened cells will be n+[X] where X is the random value "number of empty cells opened".
IF you check s_0 and it contains a prize, you check all its neighboors that could form a row/column/diagonal with it, if you hit a good one on the first try you've wasted 0 tried, if it's the second try 1 and so on. If a_i is the number of rows+column+diagonals you're checking for, so far the average will be n+1/(2n+2)(0+1+...+(a_i-1))
