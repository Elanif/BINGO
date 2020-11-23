\documentclass[1pt]{article}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage[latin1]{inputenc}
\usepackage{amssymb}
\usepackage{enumerate}

\title{Least average tries to open a bingo line}
\author{Elanif}
\date{23/11/2020}

\begin{document}
\maketitle

There's a $n\times n$ bingo board, one of the $n$ columns, $n$ rows and $2$ diagonals contains prizes, what's the best strategy to open all cells of that line? Assuming an equal chance of every $2n+2$ line being the bingo one it goes as follows.
\\
A strategy works as follows: you check a spot $s_i$, if it has the prize you check its neighbors, if it's empty you proceed to $s_{i+1}$. $\{s_i\}_{i\in \{0,\dotsc,k\}}$

The average number of opened cells will be $n+[X]$ where $X$ is the random value "number of empty cells opened".
\\
If you check $s_0$ and it contains a prize, you check all its neighbors that could form a row/column/diagonal with it, if you hit a good one on the first try you've wasted $0$ tries, if it's the second try $1$ and so on. If $a_0$ is the number of rows+column+diagonals you're checking for, so far the average will be $n+1/(2n+2)(0+1+...+(a_0-1))$.
\\

Properties of $\{a_i\}_{i\in \{0,\dotsc,k\}}$
\begin{enumerate}
\item $a_i\in\{1,2,3,4\}$.
\newline$a_i=1$ and $a_i=0$ are ideally the same: 
\newline $a_i=0$ means checking if it's the right row/column/diagonal without checking wich one of these options it is. It should only happen when checking the last option by elimination (which will be the strategy for $n=3$). 
\newline $a_i=1$ means checking a cell, then only one of its neighbors to confirm if it's a bingo. If the last option is being checked then it means $a_i$ is actually 0. If there are more lines to check then it's always better to check the intersection $s_i$ of these two lines.
\newline These last 2 options will be grouped into $a_i=1$, because the formulas work better this way.
\item[1b)] $a_i=4$ is only possible if $n$ is odd and $s_i$ is in the dead center of the board.
\item[1c)] $a_i=3$ is only possible if $s_i$ is on a diagonal but not on the center, if it exists.
\item At most 2 elements of $\{a_i\}_{i\in \{0,\dotsc,k\}}$ are $\geq 3$, since there are 2 diagonals.
\item $\displaystyle\sum_{i=0}^{k} a_i = 2n+2$
\end{enumerate}

The expected value of a strategy can be calculated with $\{a_i\}_{i\in \{0,\dotsc,k\}}$: for example let $n=5$, $s_i=i-th$ cell on a diagonal, $(a_0,a_1,a_2,a_3,a_4)=(3,2,3,2,2)$ returns an expected value of $5+1/12((0+1+2)+(1+2)+(2+3+4)+(3+4)+(4+5)) = 7+7/12$.
\newline\newline
In the general case $[X]=1/(2n+2)\sum_{i=0}^{n-1} (a_ii+a_i(a_i-1)/2)$ which is uselessly? equal to $1/(2n+2)\sum_{i=0}^{n-1} (1/2a_i(a_i+2i-1))$

Alternatively $[X]=n*(n-1)/2+1/(2n+2)\sum_{i=0}^{n-1} (i*(a_i-1)+a_i*(a_i-1)/2)$ which is uselessly? equal to $n*(n-1)/2+1/(2n+2)\sum_{i=0}^{n-1} (1/2(a_i-1)(a_i+2i))$

Let 
\[ f(\{a_i\},k)=\sum_{i=0}^{k} (a_ii+a_i(a_i-1)/2) \]
And
\[ (a_0,\dotsc,a_k) \sim (b_0,\dotsc,b_h) \iff f(\{a_i\},k)=f(\{b_j\},h)\]

To find the best strategy it means to find such $s_i$ so that $f$ is minimum.
\newline \newline
Properties of an optimal$\{a_i\}_{i\in \{0,\dotsc,k\}}$
\begin{enumerate}
\item $\{a_i\}_{i\in \{0,\dotsc,k\}}$ is descending: if $\exists i,j\in\{0,\dotsc,k\}:i<j \land a_i<a_j$. By switching $a_i$ with $a_j$ the expected value diminishes
\item At most two items in $\{a_i\}_{i\in \{0,\dotsc,k\}}$ are equal to $1$
\newline if more than $2$ existed the sequence would be of the form $(\dotsc,\underbrace{1,\dotsc,1}_\text{at least 3 times})$ and by collapsing the first 2 1's together we get a lower expected value
\newline
Note that $(a_0,\dotsc,a_{k-2},1,1)\sim(a_0,\dotsc,a_{k-2},2)$

\item $\forall n\in\mathbb{N} (n\geq2 \implies \exists i\in\{0,\dotsc,k\}: a_i\geq3)$
\newline By absurd $\forall i\in\{0,\dotsc,k\}: a_i\leq2$, then the sequence is either $A=(\underbrace{2,\dotsc,2}_\text{n+1 times})$ or $B=(\underbrace{2,\dotsc,2}_\text{n times},1,1)$.
\newline But $A \sim B$ and in both cases $(3,\underbrace{2,\dotsc,2}_\text{n-1 times},1)$ is better by $n+1-2=n-1\geq1$.
\end{enumerate}
\newline
This proves that if $n\geq2$ the best sequences are one of the following:
\begin{itemize}
\item \begin{equation} (4,\underbrace{2,\dotsc,2}_\text{n-1 times})\sim(4,\underbrace{2,\dotsc,2}_\text{n-2 times},1,1)
\end{equation}
$[X]=(n^2+5)/(2n+2)$
\item \begin{equation}(3,3,\underbrace{2,\dotsc,2}_\text{n-2 times})\sim(3,3,\underbrace{2,\dotsc,2}_\text{n-3 times},1,1)\end{equation} $[X]=(n^2+5)/(2n+2)$
\item \begin{equation}(3,\underbrace{2,\dotsc,2}_\text{n-1 times},1)\end{equation} $[X]=(n^2+n+2)/(2n+2)$
\end{itemize}

In conclusion

\begin {itemize}
\item If $n=0$ the best sequence are $(2)\sim(1,1)$, $[X]=1/2$
\item If $n=1$ the best sequences are $(3,1)\sim(2,2)\sim(2,1,1)$, $[X]=4/4=1$
\item $\forall n\in\mathbb{N}(n+2\leq5 \iff n\leq2)\implies$ for $n=2$ the best sequence is $(3,2,1$, $[X]=8/6=4/3$
\item If $n=3$ $n^2+5=n^2+n+2$ so all 5 of (1) (2) and (3) are the best, $[X]=14/8=7/4$
\item If $n\geq4$ and $n$ is odd (1) and (2) are the best sequences, If $n$ is even only (2) are. $[X]=(n^2+5)/(2n+2)$
\end{itemize}

In reality $n=0$ would be an empty bingo board $\implies [X]=0$
\newline $n=1$ doesn't have $4$ lines, but only 1, so then again $[X]=0$
\newline For $n=2$ $(3,3)$ isn't possible, and the only strategy is $(3,2,1)$ and all the cells are symmetric.
\newline

\[
  [X]= \left\{
	\begin{array}{ll}
		0 & \mbox{if } 0\leq n \leq 1 \\
		4/3 & \mbox{if } n=2 \\
		(n^2+5)/(2n+2) & \mbox{if } n\geq3 \\
	\end{array}
\right
\]
\newline
(1) is always possible when $n\geq3 \land n \text{ is odd}$: $s_0$ is the center and the subsequent $s_i$'s are all on the same diagonal.

\end{document}
