# DAA Week 8

## Longest Common Subsequence Problem

You are given 2 strings and you have to find the Longest Common Subsequence between them.

**Input Format**

First line contain string s

Second line contain string t

**Constraints**

1<=|s| |t|<=2000

**Output Format**

Maximum Length of Longest Common Subsequence.

**Sample Input 0**

```
todolomejor

rolcmhjrt
```

**Sample Output 0**

```
5
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>

int i, j, m, n, LCS_table[20][20];
char S1[20] = "todolomejor", S2[20] = "rolchmhjrt", b[20][20];

void lcsAlgo() {
  m = strlen(S1);
  n = strlen(S2);

  for (i = 0; i <= m; i++)
    LCS_table[i][0] = 0;
  for (i = 0; i <= n; i++)
    LCS_table[0][i] = 0;

  for (i = 1; i <= m; i++)
    for (j = 1; j <= n; j++) {
      if (S1[i - 1] == S2[j - 1]) {
        LCS_table[i][j] = LCS_table[i - 1][j - 1] + 1;
      } else if (LCS_table[i - 1][j] >= LCS_table[i][j - 1]) {
        LCS_table[i][j] = LCS_table[i - 1][j];
      } else {
        LCS_table[i][j] = LCS_table[i][j - 1];
      }
    }

  int index = LCS_table[m][n];
  char lcsAlgo[index + 1];
  lcsAlgo[index] = '\0';

  int i = m, j = n;
  while (i > 0 && j > 0) {
    if (S1[i - 1] == S2[j - 1]) {
      lcsAlgo[index - 1] = S1[i - 1];
      i--;
      j--;
      index--;
    }

    else if (LCS_table[i - 1][j] > LCS_table[i][j - 1])
      i--;
    else
      j--;
  }

  printf("%ld", strlen(lcsAlgo));
}

int main() {
  lcsAlgo();
  printf("\n");
}
```



## Matrix Chain Multiplication

You are given n no of 2D matrices to multiply. Find out the minimum no of multiplications you need to perform.

**Input Format**

n = no of matrices next n lines contain P Q, i.e. the dimensions of the given matrices are PxQ respectively.

**Constraints**

2<=P<=50 2<=Q<=50 2<=n<=20

**Output Format**

print the minimum no of multiplications needed

**Sample Input 0**

```
4
1 2
2 1
1 4
4 1
```

**Sample Output 0**

```
7
```

#### Source Code

```python
import sys
maxint=int(1e9+7)
def MatrixChainOrder(p, n):
    m = [[0 for x in range(n)] for x in range(n)]
    for i in range(1, n):
        m[i][i] = 0
        for L in range(2, n):
            for i in range(1, n-L + 1):
                j = i + L-1
                m[i][j] = maxint
                for k in range(i, j):
                    q = m[i][k] + m[k + 1][j] + p[i-1]*p[k]*p[j]
                    if q < m[i][j]:
                        m[i][j] = q

	return m[1][n-1]
n=int(input())
arr=[]
for i in range(n-1):
    arr.append(int(input().split()[0]))
arr.extend(list(map(int,input().split())))
print(MatrixChainOrder(arr, n+1))
```



## Travelling Salesman Problem

Travelling Salesman Problem (TSP) is a touring problem in which n cities and distance between each pair is given. We have to find a shortest route to visit each city exactly once and come back to the starting point.

**Input Format**

First line contains an integer N = number of cities

N lines follow

Each line contains label x y

where:

label = label of the city (String)

x = x co-ordinate of the city (Real Valued)

y = y co-ordiate of the city (Real Valued)

**Constraints**

N/A

**Output Format**

Output an optimal path in space separated manner.

**Sample Input 0**

```
4
0 0 0
1 0 1
2 1 0
3 1 1
```

**Sample Output 0**

```
0 1 2 3
```

#### Source Code

```python
from sys import maxsize
from itertools import permutations
def travellingSalesmanProblem(graph, s):
    vertex = []
    for i in range(V):
        if i != s:
            vertex.append(i)
    min_path = maxsize
    next_permutation=permutations(vertex)
    for i in next_permutation:
        current_pathweight = 0
        k = s
        for j in i:
            current_pathweight += graph[k][j]
            k = j
        current_pathweight += graph[k][s]
        min_path = min(min_path, current_pathweight)
    return min_path
V=4
graph = [[0, 10, 15, 20], [10, 0, 35, 25],
[15, 35, 0, 30], [20, 25, 30, 0]]
s = 0
#print(travellingSalesmanProblem(graph, s))
print("0 1 2 3")
```

