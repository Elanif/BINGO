# BINGO
Least average tries to open a bingo line

There's a n\times n bingo board, one of the n columns, n rows and 2 diagonals contains prizes, what's the best strategy to open all cells of that line? Assuming an equal chance of every 2n+2 line being the bingo one it goes as follows.

A strategy works as follows: you check a spot s_i, if it has the prize you check its neighboors, if it's empty you proceed to s_(i+1).

The average number of opened cells will be n+[X] where X is the random value "number of empty cells opened".

IF you check s_0 and it contains a prize, you check all its neighboors that could form a row/column/diagonal with it, if you hit a good one on the first try you've wasted 0 tried, if it's the second try 1 and so on. If a_0 is the number of rows+column+diagonals you're checking for, so far the average will be n+1/(2n+2)(0+1+...+(a_0-1)).

Note that a_i\in{1,2,3,4}, with a_i=4 being only possible if s_i is in the dead center of the board, if n is odd, and a_i=3 only possible if s_i is on a diagonal. An already checked off line from s_j j<i won't count for a_i.

If s_0 is empty you check s_1, you check a_1 spots, but this time you've already wasted a check on a_0, so the contribution to the expected value is 1/(2n+2)(1+2+...+(a_1-1))

The expected value of a strategy can be derived by knowing the a_i: for example let n=5, s_i=i-th cell on a diagonal, (a_0,a_1,a_2,a_3,a_4}={3,2,3,2,2} returns an expected value of 5+1/12*((0+1+2)+(1+2)+(2+3+4)+(3+4)+(4+5)) = 7+7/12-

In the general case [X]=n*(n-1)/2+\sum{i=0}^{n-1} (i*(a_i-1)+a_i*(a_i-1)/2) = n*(n-1)/2+\sum{i=0}^{n-1} (1/2(a_i-1)(a_i+2i))
