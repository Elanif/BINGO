# BINGO
Least average tries to open a bingo line

There's a <img src="https://latex.codecogs.com/gif.latex?n\times n" /> bingo board, one of the n columns, n rows and 2 diagonals contains prizes, what's the best strategy to open all boxes of that line? Assuming an equal chance of every <img src="https://latex.codecogs.com/gif.latex?2n+2" /> line being the bingo one it goes as follows.

A strategy works as follows: you check a spot <img src="https://latex.codecogs.com/gif.latex?s_i" />, if it has the prize you check its neighboors, if it's empty you proceed to s_(i+1)
