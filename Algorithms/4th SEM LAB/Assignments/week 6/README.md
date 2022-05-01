# DAA Week 6

## Kruskal's Algorithm

Given a weighted undirected graph. Find the sum of weights of edges of a Minimum Spanning Tree.

**Input Format**

Given 2 integers N and M. N represents the number of vertices in the graph. M represents the number of edges between any 2 vertices. Then M lines follow, each line has 3 space separated integers ai,bi ,wi where ai and bi represents an edge from a vertex ai to a vertex bi and wi respresents the weight of that edge.

**Constraints**

2<=N<=10000 1<=M<=100000 1<=ai,bi<=N 1<=wi<=1000

**Output Format**

Print the summation of edges weights in the MST.

**Sample Input 0**

```
4 5
1 2 7
1 4 6
4 2 9
4 3 8
2 3 6
```

**Sample Output 0**

```
19
```

#### Source Code

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Edge {
	int src, dest, weight;
};
struct Graph {
	int V, E;
	struct Edge* edge;
};
struct Graph* createGraph(int V, int E)
{
	struct Graph* graph =(struct Graph *)malloc(sizeof(struct Graph));
	graph->V = V;
	graph->E = E;
	graph->edge =(struct Edge *)malloc(E*sizeof(struct Edge));
	return graph;
}
struct subset {
	int parent;
	int rank;
};
int find(struct subset subsets[], int i)
{
	if (subsets[i].parent != i)
		subsets[i].parent = find(subsets, subsets[i].parent);
	return subsets[i].parent;
}
void Union(struct subset subsets[], int x, int y)
{
	int xroot = find(subsets, x);
	int yroot = find(subsets, y);
	if (subsets[xroot].rank < subsets[yroot].rank)
		subsets[xroot].parent = yroot;
	else if (subsets[xroot].rank > subsets[yroot].rank)
		subsets[yroot].parent = xroot;
	else
	{
	subsets[yroot].parent = xroot;
	subsets[xroot].rank++;
	}
}
int myComp(const void* a, const void* b)
{
	struct Edge* a1 = (struct Edge*)a;
	struct Edge* b1 = (struct Edge*)b;
	return a1->weight > b1->weight;
}
void KruskalMST(struct Graph* graph)
{
	int V = graph->V;
	struct Edge
	result[V];
	int e = 0;
	int i = 0;
	qsort(graph->edge, graph->E, sizeof(graph->edge[0]),myComp);
	struct subset* subsets = (struct subset*)malloc(V * sizeof(struct subset));
	for (int v = 0; v < V; ++v) {
		subsets[v].parent = v;
		subsets[v].rank = 0;
	}
	while (e < V - 1 && i < graph->E) {
		struct Edge next_edge = graph->edge[i++];
		int x = find(subsets, next_edge.src);
		int y = find(subsets, next_edge.dest);
		if (x != y) {
			result[e++] = next_edge;
			Union(subsets, x, y);
		}
	}
	int minimumCost = 0;
	for (i = 0; i < e; ++i)
    {	
		minimumCost += result[i].weight;
	}
	printf("%d",minimumCost);
	return;
}

int main()
{
	int V ;
	int E;
	scanf("%d%d",&V,&E);
	struct Graph* graph = createGraph(V, E);
	for(int i=0;i<E;i++)
	{
		int u,v,w;
		scanf("%d%d%d",&u,&v,&w);
		graph->edge[i].src=u-1; // if indexing is from 0
		graph->edge[i].dest=v-1;
		graph->edge[i].weight=w;
	}
	KruskalMST(graph);
	return 0;
}
```



## Prim's Algorithm

Given a weighted undirected graph. Find the sum of weights of edges of a Minimum Spanning Tree.

**Input Format**

Given 2 integers N and M. N represents the number of vertices in the graph. M represents the number of edges between any 2 vertices. Then M lines follow, each line has 3 space separated integers ai,bi ,wi where ai and bi represents an edge from a vertex ai to a vertex bi and wi respresents the weight of that edge.

**Constraints**

2<=N<=10000 1<=M<=100000 1<=ai,bi<=N 1<=wi<=1000

**Output Format**

Print the summation of edges weights in the MST.

**Sample Input 0**

```
4 5
1 2 7
1 4 6
4 2 9
4 3 8
2 3 6
```

**Sample Output 0**

```
19
```

#### Source Code

```c
#include<stdio.h> 
#include<stdlib.h> 
  
#define infinity 9999 
#define MAX 20 
  
int G[MAX][MAX],spanning[MAX][MAX],n; 
  
int prims(); 
  
int main() 
{ 
	int i,j,total_cost; 
	printf("Enter no. of vertices:"); 
	scanf("%d",&n); 
	printf("\nEnter the adjacency matrix:\n"); 
	for(i=0;i<n;i++) 
		for(j=0;j<n;j++) 
			scanf("%d",&G[i][j]); 
	total_cost=prims(); 
	printf("\nspanning tree matrix:\n"); 
	for(i=0;i<n;i++) 
	{ 
		printf("\n"); 
		for(j=0;j<n;j++) 
			printf("%d\t",spanning[i][j]); 
	} 
	printf("\n\nTotal cost of spanning tree=%d",total_cost); 
	return 0; 
}
int prims() 
{ 
	int cost[MAX][MAX]; 
i	nt u,v,min_distance,distance[MAX],from[MAX]; 
	int visited[MAX],no_of_edges,i,min_cost,j; 
	//create cost[][] matrix,spanning[][] 
	for(i=0;i<n;i++) 
		for(j=0;j<n;j++) 
		{ 
			if(G[i][j]==0) 
				cost[i][j]=infinity; 
			else 
				cost[i][j]=G[i][j]; 
			spanning[i][j]=0; 
		} 
	//initialise visited[],distance[] and from[] 
	distance[0]=0; 
	visited[0]=1; 
	for(i=1;i<n;i++) 
	{ 
		distance[i]=cost[0][i]; 
		from[i]=0; 
		visited[i]=0; 
	} 
	min_cost=0; //cost of spanning tree 
	no_of_edges=n-1; //no. of edges to be added 
	while(no_of_edges>0) 
	{ 
	//find the vertex at minimum distance from the tree 
		min_distance=infinity;
		for(i=1;i<n;i++) 
			if(visited[i]==0&&distance[i]<min_distance) 
			{ 
				v=i; 
				min_distance=distance[i]; 
			} 
		u=from[v]; 
		//insert the edge in spanning tree 
		spanning[u][v]=distance[v]; 
		spanning[v][u]=distance[v]; 
		no_of_edges--; 
		visited[v]=1; 
		//updated the distance[] array 
		for(i=1;i<n;i++) 
		if(visited[i]==0&&cost[i][v]<distance[i]) 
		{ 
			distance[i]=cost[i][v]; 
			from[i]=v; 
		} 
		min_cost=min_cost+cost[u][v]; 
	} 
	return(min_cost); 
}
```

