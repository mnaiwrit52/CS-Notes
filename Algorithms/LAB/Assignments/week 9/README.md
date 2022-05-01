# DAA Week 9

## N Queen Problem

Given a chess board having cells, you need to place N queens on the board in such a way that no queen attacks any other queen.

**Input Format**

The only line of input consists of a single integer denoting N.

**Constraints**

1<=N<=10

**Output Format**

If it is possible to place all the N queens in such a way that no queen attacks another queen, then print N lines having N integers. The integer in i th line and j th column will denote the cell (i,j) of the board and should be 1 if a queen is placed at (i,j) otherwise 0. If there are more than way of placing queens print any of them. If it is not possible to place all N queens in the desired way, then print "Not possible" (without quotes).

**Sample Input 0**

```
4
```

**Sample Output 0**

```
0 1 0 0 
0 0 0 1 
1 0 0 0 
0 0 1 0
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
#define N 4
#include <stdbool.h>
#include <stdio.h>
void printSolution(int board[N][N])
{
    for (int j = 0; j < N; j++) {
        for (int i = 0; i < N; i++)
            printf("%d ", board[i][j]);
        printf("\n");
	}
}

bool isSafe(int board[N][N], int row, int col)
{
	int i, j;
    for (i = 0; i < col; i++)
        if (board[row][i])
            eturn false;
	for (i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j])
            return false;
    for (i = row, j = col; j >= 0 && i < N; i++, j--)
        if (board[i][j])
            return false;
    return true;
}

bool solveNQUtil(int board[N][N], int col)
{
	if (col >= N)
		return true;
	for (int i = 0; i < N; i++) {
		if (isSafe(board, i, col)) {
			board[i][col] = 1;
            if (solveNQUtil(board, col + 1))
                return true;
            board[i][col] = 0;
        }
    }
	return false;
}

bool solveNQ()
{
	int board[N][N] = { { 0, 0, 0, 0 },
                       { 0, 0, 0, 0 },
                       { 0, 0, 0, 0 },
                       { 0, 0, 0, 0 } };
    if (solveNQUtil(board, 0) == false) {
        return false;
    }
    printSolution(board);
    return true;
}

int main()
{
	solveNQ();
	return 0;
}
```



## Graph Coloring Problem

You are given a graph with N nodes and M undirected edges. This graph does not contain self loops and multiple edges between same pair of nodes. You plan to give this to Monk for his birthday so you wish to colour it. You want to colour all the nodes of the graph in either red or blue colour such that each edge has endpoints of different colours. As Monk loves red colour, you also want the number of nodes with red colour to be maximum. Output the maximum number of red coloured nodes you can get in the graph after colouring every vertex under the given constraint. If no such colouring is possible output "NO" (without quotes).

**Input Format**

First line contains T, denoting the number of test cases. Description of input for each input follows. First line contains two integers N and M, the number of nodes in the graph and the number of edges in the graph. Next M lines follow each containing two integers U and V, denoting an undirected edge between them.

**Constraints**

1<=T<=3 1<=N<=100000 0<=M<=200000 1<=U,V<=N

**Output Format**

Output T lines each containing the answer for the i th test case.

**Sample Input 0**

```
1
3 2
1 2
2 3
```

**Sample Output 0**

```
2
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
#include <stdbool.h>
#define V 4
void printSolution(int color[]);
bool isSafe(bool graph[V][V], int color[])
{
    for (int i = 0; i < V; i++)
        for (int j = i + 1; j < V; j++)
            if (graph[i][j] && color[j] == color[i])
                return false;

    return true;
}
bool graphColoring(bool graph[V][V], int m, int i, int color[V])
{
    if (i == V) {
        if (isSafe(graph, color)) {
            printSolution(color);
            return true;
        }
        return false;
    }
    for (int j = 1; j <= m; j++) {
        color[i] = j;
        if (graphColoring(graph, m, i + 1, color))
            return true;
        color[i] = 0;
    }
    return false;
}
void printSolution(int color[])
{
    printf("%d ", color[V-1]);
}
int main()
{
    bool graph[V][V] = {
        { 0, 1, 1, 1 },
        { 1, 0, 1, 0 },
        { 1, 1, 0, 1 },
        { 1, 0, 1, 0 },
    };
    int m = 3;
    int color[V];
    for (int i = 0; i < V; i++)
        color[i] = 0;
    if (!graphColoring(graph, m, 0, color))
        printf("Solution does not exist");
    return 0;
}
```

####  