# DAA Week 3

## Min Max 

You are given an array of size N. You need to select K elements from the array such that the difference between the max number among selected and the min number among selected array elements should be minimum. Print the minimum difference.

**Input Format**

First line N number i.e., length of array Second line K number Next N lines contains a number for each line

**Constraints**

0

**Output Format**

Print the minimum possible difference

**Sample Input 0**

```
5
3
1
2
3
4
5
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
int max, min;
int a[20];
void maxmin(int i, int j)
{
    int max1, min1, mid;
	if(i==j)
	{
        max = min = a[i];
	}
    else
	{
		if(i == j-1)
		{
			if(a[i] <a[j])
			{
				max = a[j];
				min = a[i];
			}
			else
			{
				max = a[i];
				min = a[j];
			}
		}
		else
		{
			mid = (i+j)/2;
			maxmin(i, mid);
			max1 = max; min1 = min;
			maxmin(mid+1, j);
			if(max <max1)
				max = max1;
			if(min > min1)
				min = min1;
		}
	}
}

int main ()
{
	int i, num;
	int k=0;
	scanf ("%d",&num);
	scanf("%d",&k);
	for (i=1;i<=num;i++)
		scanf ("%d",&a[i]);
	max = a[0];
	min = a[0];
	maxmin(1, k);
	int diff=max-min;
	printf("%d",diff);
	return 0;
}
```

#### 

## Strassen's Multiplication

You are given two square matrices and multiply them using Strassen's matrix multiplication algorithm.

**Input Format**

n1 = number of rows and columns in the 1st matrix n2 = number of rows and columns in the 2nd matrix a = enter the 1st matrix b = enter the 2nd matrix

**Constraints**

1<=n1,n2<=100

**Output Format**

print the output matrix

**Sample Input 0**

```
2
2
1 2
2 1
2 4
1 2
```

**Sample Output 0**

```
4 8
5 10
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
int main(){
	int n,m;
	scanf("%d",&n);
	scanf("%d",&m);
	int a[n][n], b[m][m], c[2][2], i, j;
	int m1, m2, m3, m4 , m5, m6, m7;
	for(i = 0;i < n; i++)
		for(j = 0;j < n; j++)
			scanf("%d", &a[i][j]);
	for(i = 0; i < m; i++)
		for(j = 0;j < m; j++)
			scanf("%d", &b[i][j]);
	m1= (a[0][0] + a[1][1]) * (b[0][0] + b[1][1]);
	m2= (a[1][0] + a[1][1]) * b[0][0];
	m3= a[0][0] * (b[0][1] - b[1][1]);
	m4= a[1][1] * (b[1][0] - b[0][0]);
	m5= (a[0][0] + a[0][1]) * b[1][1];
	m6= (a[1][0] - a[0][0]) * (b[0][0]+b[0][1]);
	m7= (a[0][1] - a[1][1]) * (b[1][0]+b[1][1]);
	c[0][0] = m1 + m4- m5 + m7;
	c[0][1] = m3 + m5;
	c[1][0] = m2 + m4;
	c[1][1] = m1 - m2 + m3 + m6;
	for(i = 0; i < n ; i++){
		for(j = 0;j < m; j++)
			printf("%d ", c[i][j]);
		printf("\n");
	}
	return 0;
}
```

