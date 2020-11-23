\documentclass[1pt]{article}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage[latin1]{inputenc}
\usepackage{amssymb}

\title{Least average tries to open a bingo line}
\author{Elanif}
\date{23/11/2020}

\begin{document}
\maketitle

There's a $n\times n$ bingo board, one of the $n$ columns, $n$ rows and $2$ diagonals contains prizes, what's the best strategy to open all cells of that line? Assuming an equal chance of every $2n+2$ line being the bingo one it goes as follows.
\\
A strategy works as follows: you check a spot $s_i$, if it has the prize you check its neighboors, if it's empty you proceed to $s_{i+1}$. $\{s_i\}_{i\in \{1,\dotsc,k\}}$

The average number of opened cells will be $n+[X]$ where $X$ is the random value "number of empty cells opened".
\\
If you check $s_0$ and it contains a prize, you check all its neighboors that could form a row/column/diagonal with it, if you hit a good one on the first try you've wasted $0$ tries, if it's the second try $1$ and so on. If $a_0$ is the number of rows+column+diagonals you're checking for, so far the average will be $n+1/(2n+2)(0+1+...+(a_0-1))$.
\\

Properties of $\{a_i\}_{i\in \{1,\dotsc,k\}}$
\begin{enumerate}
\item $a_i\in\{1,2,3,4\}$, $a_i=4$ being only possible if $s_i$ is in the dead center of the board and if $n$ is odd, and $a_i=3$ only possible if $s_i$ is on a diagonal.
\item All the elements except $1$ or $2$ of $\{a_i\}_{i\in \{1,\dotsc,k\}}$ are $\leq 2$
\newline $a_i=4 \iff s_i$ is on the dead center of the board
\newline $a_j = 3 \iff s_j$ is on a diagonal but not the center
\item $\displaystyle\sum_{i=0}^{k} a_i = 2n+2$
\end{enumerate}

The expected value of a strategy can be calculated with $\{a_i\}_{i\in \{1,\dotsc,k\}}$: for example let $n=5$, $s_i=i-th$ cell on a diagonal, $(a_0,a_1,a_2,a_3,a_4)=(3,2,3,2,2)$ returns an expected value of $5+1/12((0+1+2)+(1+2)+(2+3+4)+(3+4)+(4+5)) = 7+7/12$.
\newline\newline
In the general case $[X]=1/(2n+2)\sum_{i=0}^{n-1} (a_ii+a_i(a_i-1)/2)$ which is uselessly? equal to $1/(2n+2)\sum_{i=0}^{n-1} (1/2a_i(a_i+2i-1))$

Alternatively $[X]=n*(n-1)/2+1/(2n+2)\sum_{i=0}^{n-1} (i*(a_i-1)+a_i*(a_i-1)/2)$ which is uselessly? equal to $n*(n-1)/2+1/(2n+2)\sum_{i=0}^{n-1} (1/2(a_i-1)(a_i+2i))$

Let 
\[ f(\{a_i\},k)=1/(2n+2)\sum_{i=0}^{n-1} (a_ii+a_i(a_i-1)/2) \]

To find the best strategy it means to find such $s_i$ so that $f$ is minimum.
\newline \newline
Properties of an optimal$\{a_i\}_{i\in \{1,\dotsc,k\}}$
\begin{enumerate}
\item $\{a_i\}_{i\in \{1,\dotsc,k\}}$ is descending: if $\exists i,j\in\{1,\dotsc,k\}:i<j \land a_i<a_j$. By switching $a_i$ with $a_j$ the expected value diminishes
\item At most two items in $\{a_i\}_{i\in \{1,\dotsc,k\}}$ are equal to $1$
\newline if more than $2$ existed the sequence would be of the form $(\dotsc,\underbrace{1,\dotsc,1}_\text{at least 3 times})$ and by collapsing the first 2 1's together we get a lower expected value

\item $\forall n\in\mathbb{N} (n\geq2 \implies \exists i\in\{1,\dotsc,k\}: a_i\geq3)$
\newline By absurd $\forall i\in\{1,\dotsc,k\}: a_i\leq2$, then the sequence is either $(\underbrace{2,\dotsc,2}_\text{n+1 times})$ or $(\underbrace{2,\dotsc,2}_\text{n times},1,1)$
\end{enumerate}

This proves that the best sequences are $(4,\underbrace{2,\dotsc,2}_\text{n-1 times})$ or  $(3,3,\underbrace{2,\dotsc,2}_\text{n-2 times})$, in both cases $[X]=$

\end{document}


\newline If $n=2$ the optimal strategy is $(4,2)$ or $(3,3)$
\newline If $n=3$ the optimal strategy is $(4,2,2)$ or $(3,3,2)$
\newline If $n\geq4$ since the sum of $a_i$ is even there either are (a) $3$ and $1$ or (b) $1$ and $1$ in the sequence
\newline If (a) holds the sequence is of the form $(3,2,\dotsc,2,1)$, and by collapsing the $1$ onto the first $2$ we obtain $(3,3,2,\dotsc,2)$ which is more optimal.
\newline if (b) holds the sequence is of the form $(4,2,\dotsc,1,1)$ or $(3,3,\dotsc,1,1)$, but by collapsing the 2 1's together the expected value doesn't change
\underbrace{\dotsc}_\text{0 to 1 times
