# DAA Week 4

## Breadth First Search (BFS)

Given an adjacency matrix representation of a graph, compute the shortest path from a source vertex to a goal vertex using Breadth First Search. In case of a tie, a smaller indexed vertex should be preferable to a larger indexed vertex.

**Input Format**

The first line is the number of test cases. Thereafter, for every test case, the first line of input is n, the number of vertices in the graph. Then n lines of inputs have n integers each, separated by a space, denoting the adjacency matrix. The next line of input is the index of source and goal, the indexing starts from 0.

**Constraints**

NA

**Output Format**

The first line of output is the cost of shortest path from source to goal. The second line of output is the path from source to goal (including both source and goal).

**Sample Input 0**

```
1

5

0 1 1 0 0

1 0 1 0 0

1 1 0 1 0

0 0 1 0 1

0 0 0 1 0

0 4
```

**Sample Output 0**

```
3

0 2 3 4
```

#### Source Code

```c
#include <stdio.h>
int graph[100][100], q[100], prev[100], visited[100], front = 0, rear = 0;
int bfs(int vertex, int total, int endvertex){
	while (front <= rear){
		visited[vertex] = 1;
		for (int i = 1; i <= total; i++){
			if (graph[vertex][i] == 1 && visited[i] == 0){
				visited[i] = 1;
				prev[i] = vertex;
				q[rear] = i;
				rear++;
			}
		}
		vertex = q[front];
		front++;
		if (vertex == endvertex){
			return 1;
		}
	}
	return 0;
}

int main(){
	int n;
	scanf("%d", &n);
	for (int tc = 0; tc < n; tc++){
		int total, starting, ending;
		scanf("%d", &total);
		for (int i = 1; i <= total; i++){ // O(total Vertices)
			prev[i] = -1;
			visited[i] = 0;
		}
		for (int i = 1; i <= total; i++){ // O(total Vertices^2)
			for (int j = 1; j <= total; j++){
				scanf("%d", &graph[i][j]);
			}
		}
		scanf("%d %d", &starting, &ending);
		starting += 1;
		ending += 1;
		int flag = bfs(starting, total, ending); // O(total Vertices^2)
		int path[105] = {0};
		int ctr = 0;
		if (flag == 1){
			while (prev[ending] != -1){
				path[ctr] = ending;
				ending = prev[ending];
				ctr++;
			}
			printf("%d\n\n", ctr);
			printf("%d", starting - 1);
			for (int i = ctr - 1; i >= 0; i--){
				printf(" %d", path[i] - 1);
			}
			puts("");
		}
		else {
			printf("Not found\n");
		}
	}
	return 0;
}
```



## Depth First Search (DFS)

You have been given a graph consisting of N nodes and M edges. The nodes in this graph are enumerated from 1 to N . The graph can consist of self-loops as well as multiple edges. This graph consists of a special node called the head node. You need to consider this and the entry point of this graph. You need to find and print the number of nodes that are unreachable from this head node.

**Input Format**

The first line consists of a 2 integers N and M denoting the number of nodes and edges in this graph. The next M lines consist of 2 integers a and b denoting an undirected edge between node a and b. The next line consists of a single integer x denoting the index of the head node.

**Constraints**

1<=N<=10^5 1<=M<=10^5 1<=x<=N

**Output Format**

You need to print a single integer denoting the number of nodes that are unreachable from the given head node.

**Sample Input 0**

```
10 10
8 1
8 3
7 4
7 5
2 6
10 7
2 8
10 9
2 10
5 10
2
```

**Sample Output 0**

```
0
```

#### Source Code

```c
#include<stdio.h>
#include<stdlib.h>
typedef struct node
{
	struct node *next;
	int vertex;
}node;
node *G[20];
int visited[20];
int n;
void read_graph();
void insert(int,int);
void DFS(int);
int main()
{
	int i;
	read_graph();
	for(i=0;i<n;i++)
		visited[i]=0;
	DFS(0);
}
void DFS(int i)
{
	node *p;
	printf("%d",i);
	p=G[i];
	visited[i]=1;
	while(p!=NULL)
	{
		i=p->vertex;
		if(!visited[i])
			DFS(i);
		p=p->next;
	}
}
void read_graph()
{
	int i,vi,vj,no_of_edges;
	scanf("%d",&n);
	for(i=0;i<n;i++)
	{
		G[i]=NULL;
		scanf("%d",&no_of_edges);
		for(i=0;i<no_of_edges;i++)
		{
			scanf("%d%d",&vi,&vj);
			insert(vi,vj);
		}
	}
}
void insert(int vi,int vj)
{
	node *p,*q;
    q=(node*)malloc(sizeof(node));
	q->vertex=vj;
	q->next=NULL;
	if(G[vi]==NULL)
		G[vi]=q;
	else
	{
		p=G[vi];
		while(p->next!=NULL)
		p=p->next;
		p->next=q;
	}
}
```

