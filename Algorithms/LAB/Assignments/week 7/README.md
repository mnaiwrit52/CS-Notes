# DAA Week 7

## 0/1 Knapsack Using Dynamic Programming

You are given n elements. Price and weight of each element is also given. You can only have items of total weight W. Calculate the total price of the products that we can have using 0-1 knapsack algorithm.

**Input Format**

n = no of items W = maximum weight that you can have cost[][]= 1st row contains the weights of the items, 2nd row contains the prices of the corresponding items.

**Constraints**

50<=W<=100
2<=n<=15

**Output Format**

Total price of the final items

**Sample Input 0**

```
3
50
10 20 30
60 100 120
```

**Sample Output 0**

```
220
```

#### Source Code

```c
#include<stdio.h>
int max(int a, int b) { return (a > b)? a : b; }
int knapSack(int W, int wt[], int val[], int n)
{
	int i, w;
	int K[n+1][W+1];
	for (i = 0; i <= n; i++)
	{
		for (w = 0; w <= W; w++)
		{
			if (i==0 || w==0)
				K[i][w] = 0;
			else if (wt[i-1] <= w)
				K[i][w] = max(val[i-1] + K[i-1][w-wt[i-1]], K[i-1][w]);
			else
				K[i][w] = K[i-1][w];
		}
	}
	return K[n][W];
}

int main()
{
	int i, n, val[20], wt[20], W;
	scanf("%d", &n);
	scanf("%d", &W);
	for(i = 0; i < n; ++i){
		scanf("%d", &wt[i]);
	}
	for(i = 0;i < n; ++i){
		scanf("%d", &val[i]);
	}
	printf("%d", knapSack(W, wt, val, n));
	return 0;
}
```



## Bellman Ford

You are given a graph with n vertices and the edges can have negative weights. Now find the shortest distance for each of the vertices from vertex 1 (that is the 1st vertex of the graph)

**Input Format**

n = no of nodes cost[][]= given cost matrix of the graph

**Constraints**

3<=n<=10 -50<=cost[i][j]<=50

**Output Format**

dist[] = one dimensional array representing the shortest distance of each vertex from the source vertex.

**Sample Input 0**

```
5
0 -1 4 0 0
0 0 3 2 2
0 0 0 0 0
0 1 5 0 0
0 0 0 -3 0
```

**Sample Output 0**

```
0 -1 2 -2 1
```

#### Source Code

```c
#include <stdio.h>
#include <stdlib.h>
int Bellman_Ford(int G[20][20] , int V, int E, int edge[20][2])
{
	int i,u,v,k,distance[20],S =1,flag=1;
	for(i=0;i<V;i++)
		distance[i] = 1000;
	distance[S-1]=0 ;
	for(i=0;i<V-1;i++)
    {
		for(k=0;k<E;k++)
		{
			u = edge[k][0] , v = edge[k][1] ;
			if(distance[u]+G[u][v] < distance[v])
				distance[v] = distance[u] + G[u][v];
		}
	}
	for(k=0;k<E;k++)
	{
		u = edge[k][0] , v = edge[k][1] ;
		if(distance[u]+G[u][v] < distance[v])
			flag = 0 ;
	}
	if(flag)
		for(i=0;i<V;i++)
			printf("%d ",distance[i]);
	return flag;
}
int main()
{
	int V,edge[20][2],G[20][20],i,j,k=0;
	scanf("%d",&V);
	for(i=0;i<V;i++)
		for(j=0;j<V;j++)
		{
			scanf("%d",&G[i][j]);
			if(G[i][j]!=0)
				edge[k][0]=i,edge[k++][1]=j;
		}
	Bellman_Ford(G,V,k,edge);
	return 0;
}
```



## Floyd Warshall

You are given a graph with n vertices. Find all pair shortest paths for that graph

**Input Format**

n = no of vertices cost[] = cost matrix

**Constraints**

3<=n<=10
1<=cost[i]<=50

**Output Format**

min_cost[][] = cost matrix containing the all pair shortest paths

**Sample Input 0**

```
4
0 11 1 6
11 0 7 3
1 7 0 2
6 3 2 0
```

**Sample Output 0**

```
0 6 1 3
6 0 5 3
1 5 0 2
3 3 2 0
```

#### Source Code

```c
#include <stdio.h>

#define V 4

#define INF 99999

void printSolution(int dist[][V]);

void floydWarshall (int graph[][V]){
    int dist[V][V], i, j, k;
    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            dist[i][j] = graph[i][j];
    for (k = 0; k < V; k++){
        for (i = 0; i < V; i++){
            for (j = 0; j < V; j++){
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }
    printSolution(dist);
}

void printSolution(int dist[][V]){
    for (int i = 0; i < V; i++){
        for (int j = 0; j < V; j++){
            if (dist[i][j] == INF)
                printf("%s", "INF");
            else
                printf ("%d ", dist[i][j]);
        }
        printf("\n");
    }
}

int main(){
    int graph[V][V] = {{0, 11, 1, 6},
                       {11, 0, 7, 3},
                       {1, 7, 0, 2},
                       {6, 3, 2, 0}};
    floydWarshall(graph);
    return 0;
}
```

