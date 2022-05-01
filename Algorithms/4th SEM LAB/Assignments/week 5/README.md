# DAA Week 5

## Knapsack 0/1

You are given n elements. Price and weight of each element is also given. You can only have items of total weight W. Calculate the total price of the products that we can have using 0-1 knapsack algorithm.

**Input Format**

n = no of items
W = maximum weight that you can have
cost[][]= 1st row contains the weights of the items, 2nd row contains the prices of the corresponding items.

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
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

// Recursive Top Down approach

int knapSack(int wts[], int prices[], int n, int w){
	if(n==0 || w==0){return 0;}
	int include=0, exclude=0;
	int result=0;
	if(wts[n-1] <= w){
		include = prices[n-1] + knapSack(wts, prices, n-1, w-wts[n-1]);
	}
	exclude = knapSack(wts, prices, n-1, w);
	if(include>exclude){
		result = include;
	}
	else{
		result = exclude;
	}
	return result;
}

int main() {
	int n, w;
	scanf("%d",&n);
	scanf("%d", &w);
	int wts[n], prices[n];
	for(int i=0;i<n;i++){
		scanf("%d", &wts[i]);
	}
	for(int i=0;i<n;i++){
		scanf("%d", &prices[i]);
	}
	printf("%d",knapSack(wts, prices, n, w));
}
```



## Fractional Knapsack

In Fractional Knapsack, we can break items for maximizing the total value of knapsack. This problem in which we can break an item is also called the fractional knapsack problem. You are given n elements. Price and weight of each element is also given. Calculate the total price of the products that we can have using fractional knapsack algorithm.

**Input Format**

n = no of items W = maximum weight that you can have cost[][]= 1st row contains the weights of the items, 2nd row contains the prices of the corresponding items

**Constraints**

50<=W<=100 2<=n<=15

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
240
```

#### Source Code

```c
#include <stdio.h>
int main()
{
    int capacity, no_items, cur_weight, item;
	int used[10];
	int total_profit;
	int i;
	int weight[10];
	int value[10];
	scanf("%d", &no_items);
	scanf("%d", &capacity);
	for (i = 0; i < no_items; i++)
	{
		scanf("%d", &weight[i]);
	}
	for (i = 0; i < no_items; i++)
	{
		scanf("%d", &value[i]);
	}
	for (i = 0; i < no_items; ++i)
		used[i] = 0;
	cur_weight = capacity;
	while (cur_weight > 0)
	{
		item = -1;
		for (i = 0; i < no_items; ++i)
		if ((used[i] == 0) && ((item == -1) || ((float) value[i] / weight[i] > (float) value[item] / weight[item])))
				item = i;
		used[item] = 1;
		cur_weight -= weight[item];
		total_profit += value[item];
		if(cur_weight<0){
				int item_percent = (int) ((1 + (float) cur_weight / weight[item]) * 100);
				total_profit -= value[item];
				total_profit += (1 + (float)cur_weight / weight[item]) * value[item];
		}
	}
	printf("%d", total_profit);
	return 0;
}
```



## Activity Selection

You are given n activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time.

**Input Format**

n = no of activities start[] = array holding the start times of the activities finish[] = array holding the finish times of the activities

**Constraints**

2<=n<=50 1<=start[i],finish[i]<=100

**Output Format**

Print the no of activity that can be performed by a single person

**Sample Input 0**

```
3
10 12 20
20 25 30
```

**Sample Output 0**

```
2
```

#### Source Code

```c
#include<stdio.h>
void printMaxActivities(int s[], int f[], int n)
{
	int i, j,k;
	//printf ("Following activities are selected n");
	i = 0,k=1;
	//printf("%d ", i);
	for (j = 1; j < n; j++)
	{
		if (s[j] >= f[i])
		{
            i = j;
			k++;
		}
	}
	printf ("%d ",k);
}

int main()
{
	int n;
	scanf("%d",&n);
	int s[n];
	int f[n];
	for(int i=0;i<n;i++)
	{
		scanf("%d",&s[i]);
	}
	for(int i=0;i<n;i++)
	{
		scanf("%d",&f[i]);
	}
	printMaxActivities(s, f, n);
	return 0;
}
```



## Optimal Merge Pattern

Optimal merge pattern is a pattern that relates to the merging of two or more sorted files in a single sorted file. This type of merging can be done by the two-way merging method.

If we have two sorted files containing n and m records respectively then they could be merged together, to obtain one sorted file in time O (n+m).

**Input Format**

Given a set of unsorted files

**Constraints**

NA

**Output Format**

Find Optimal cost

**Sample Input 0**

```
5, 3, 2, 7, 9, 13
```

**Sample Output 0**

```
93
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
#include<limits.h>
#define N 104
#define max(x, y) (((x) > (y)) ? (x) : (y))
#define min(x, y) (((x) < (y)) ? (x) : (y))

int minMergeCost(int i, int j, int* arr)
{
	int dp[N][N];
	_Bool v[N][N];
	if (i == j) return 0;
	if (v[i][j]) return dp[i][j];
	v[i][j] = 1;
	int x = dp[i][j];
	x = INT_MAX;
	int tot = 0;
	for (int k = i; k <= j; k++)
		tot += arr[k];
	for (int k = i + 1; k <= j; k++) {
		x = min(x, tot + minMergeCost(i, k - 1, arr)+ minMergeCost(k, j, arr));
	}
	return x;
}

// Driver code
int main()
{
	int arr[] = { 5, 3, 2, 7, 9, 13};
	int n = sizeof(arr) / sizeof(int);
	printf("%d",minMergeCost(0, n - 1, arr));
	return 0;
}
```

