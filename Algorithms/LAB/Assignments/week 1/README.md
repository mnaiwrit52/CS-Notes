# Week 1

## Linear Search

You have been given an array of size N consisting of integers. In addition you have been given an element M you need to find and print the index of the last occurrence of this element M in the array if it exists in it, otherwise print -1. Consider this array to be 1 indexed.

**Input Format**

The first line consists of 2 integers N and M denoting the size of the array and the element to be searched for in the array respectively . The next line contains N space separated integers denoting the elements of of the array.

**Constraints**

1<=N<=10^5 1<=A[i]<=10^9 1<=M<=10^9

**Output Format**

Print a single integer denoting the index of the last occurrence of integer M in the array if it exists, otherwise print -1.

**Sample Input 0**

```
5 1
1 2 3 4 1
```

**Sample Output 0**

```
5
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

int main() {
    
    int i = 0, flag = 0;
    
    int N, M;
    scanf("%d",&N);
    scanf("%d",&M);
    
    int arr[100000];
    
    for(i = 0; i < N; i++){
        scanf("%d ",&arr[i]);
    }
    
    for(i = 0; i < N; i++){
        if(arr[i] == M)
            flag++;
    }
    
    if(flag > 0)
        printf("%d",i);
    else
        printf("-1");
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */    
    return 0;
}
```



## Binary Search

You have been given an array A consisting of N integers. All the elements in this array A are unique. You have to answer some queries based on the elements of this array. Each query will consist of a single integer x. You need to print the rank based position of this element in this array considering that the array is 1 indexed. The rank based position of an element in an array is its position in the array when the array has been sorted in ascending order.

Note: It is guaranteed that all the elements in this array are unique and for each x belonging to a query, value x shall exist in the array

**Input Format**

The first line consists of a single integer N denoting the size of array A. The next line contains N unique integers, denoting the content of array A. The next line contains a single integer q denoting the number of queries. Each of the next q lines contains a single integer x denoting the element whose rank based position needs to be printed.

**Constraints**

1<=N<=10^5 1<=A[i]<=10^9 1<=q<=10^5 1<=x<=10^9

**Output Format**

You need to print q integers denoting the answer to each query.

**Sample Input 0**

```
5
1 2 3 4 5
5
1
2
3
4
5
```

**Sample Output 0**

```
1
2
3
4
5
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

int binarySearch(int q, int N, int *);

int main() {
    
    int i = 0;
    int N;
    
    int arr[100000];
    
    scanf("%d",&N);
    for(i = 0; i < N; i++){
        scanf("%d",&arr[i]);
    }
    
    int X;
    
    scanf("%d",&X);
    
    while(X--){
        int q;
        scanf("%d",&q);
        printf("%d\n",binarySearch(q, N, arr));
    }
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */    
    return 0;
}

int binarySearch(int q, int N, int *arr){
    int lo = 0;
    int hi = N-1;
    
    while(lo <= hi){
        int mid = (lo+hi)/2;
        
        if(arr[mid] == q)
            return mid+1;
        else if(arr[mid] < q)
            lo = mid + 1;
        else
            hi = mid - 1;
    }
    return -1;
}

```



## Insertion Sort

You have been given an A array consisting of N integers. All the elements in this array are guaranteed to be unique. For each position i in the array A you need to find the position A[i] should be present in, if the array was a sorted array. You need to find this for each i and print the resulting solution.

**Input Format**

The first line contains a single integer N denoting the size of array A. The next line contains N space separated integers denoting the elements of array A.

**Constraints**

1<=N<=100 1<=A[i]<=100

**Output Format**

Print N space separated integers on a single line , where the Ith integer denotes the position of if this array were sorted.

**Sample Input 0**

```
5
1 2 3 4 5
```

**Sample Output 0**

```
1 2 3 4 5
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
 
void insertionSort(int arr[], int n)
{
    int i, key, j;
    for (i = 1; i < n; i++)
     {
        key = arr[i];
        j = i - 1;

        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
 

int main()
{

    int n;
    scanf("%d",&n);

    int arr[n];
    for (int i = 0; i < n; i++)
    {
        scanf("%d",&arr[i]);
    } 
    insertionSort(arr, n);
    int i;
    for (i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return 0;
}

```



## Selection Sort

Consider an Array a of size N Iterate from 1 to N In ith iteration select the i th minimum and swap it with a[i]

You are given an array a, size of the array N and an integer x. Follow the above algorithm and print the state of the array after x iterations have been performed.

**Input Format**

The first line contains two integer N and x denoting the size of the array and the steps of the above algorithm to be performed respectively. The next line contains N space separated integers denoting the elements of the array.

**Constraints**

1<=N<=100 1<=a[i]<=100 1<=x<=N

**Output Format**

Print N space separated integers denoting the state of the array after x steps

**Sample Input 0**

```
5 2
1 2 3 4 5
```

**Sample Output 0**

```
1 2 3 4 5
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

int main() {
    int n;
    scanf("%d", &n);
    
    int x;
    scanf("%d", &x);
    
    int i = 0, j = 0;
    
    int arr[100];
    
    for(i = 0; i < n; i++){
        scanf("%d",&arr[i]);
    }
    
    for(i = 0; i < x; i++){
        int min = i;
        for(j = i+1; j < n; j++){
            if(arr[j] < arr[min]){
                min = j;
            }
        }
        int temp = arr[min];
        arr[min] = arr[i];
        arr[i] = temp;
    }
    
    for(i = 0; i < n-1; i++){
        printf("%d ",arr[i]);
    }
    printf("%d",arr[i]);
    
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */    
    return 0;
}

```



## Bubble Sort

You have been given an array A of size N . you need to sort this array non-decreasing oder using bubble sort. However, you do not need to print the sorted array . You just need to print the number of swaps required to sort this array using bubble sort

**Input Format**

The first line consists of a single integer N denoting size of the array. The next line contains N space separated integers denoting the elements of the array.

**Constraints**

1<=N<=100 1<=a[i]<=100

**Output Format**

Print the required answer in a single line

**Sample Input 0**

```
5
1 2 3 4 5
```

**Sample Output 0**

```
0
```

#### Source Code

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

int main()
{
    int array[100], n, i, j, ctr = 0;
    scanf("%d", &n);

    for (i = 0; i < n; i++)
        scanf("%d", &array[i]);

    for (i = 0; i < n - 1; i++)
    {
        int swap = 0;
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                int temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
                swap++;
                ctr++;
            }
        }
        
        if(swap == 0)
            break;
    }

    printf("%d", ctr);

    return 0;
}

```

