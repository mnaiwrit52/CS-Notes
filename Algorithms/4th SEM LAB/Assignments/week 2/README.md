# DAA Week 2

## Merge Sort

Merge sort is a divide-and-conquer algorithm based on the idea of breaking down a list into several sub-lists until each sublist consists of a single element and merging those sublists in a manner that results into a sorted list.

Idea:

```
Divide the unsorted list into N sublists, each containing 1 element.

Take adjacent pairs of two singleton lists and merge them to form a list of 2        elements.N will now convert into N/2 lists of size 2.
Repeat the process till a single sorted list of obtained.
```

While comparing two sublists for merging, the first element of both lists is taken into consideration. While sorting in ascending order, the element that is of a lesser value becomes a new element of the sorted list. This procedure is repeated until both the smaller sublists are empty and the new combined sublist comprises all the elements of both the sublists.

**Input Format**

First line contains one integer, N, size of array. Second line contains N space separated integers denoting the elements of the array A.

**Constraints**

1<=N<=10^6 1<=A[i]<=10^6

**Output Format**

Output will be sorted order

**Sample Input 0**

```
5
1 4 3 2 5
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
 
void mergeSort(int a[],int i,int j);
void merge(int a[],int i1,int j1,int i2,int j2); 

int main()
{
    int a[30],n,i;
    scanf("%d",&n);
    for(i = 0; i < n; i++)
        scanf("%d",&a[i]);

    mergeSort(a,0,n-1);

    for(i = 0; i < n; i++)
        printf("%d ",a[i]);
    
    return 0;
}
 
void mergeSort(int a[],int i,int j)
{
    int mid;
    if(i < j){
        mid=(i+j)/2;
        mergeSort(a, i, mid);
        mergeSort(a, mid+1, j);
        merge(a, i, mid, mid+1, j);
    }
}
 
void merge(int a[],int i1,int j1,int i2,int j2)
{
    int temp[50]; 
    int i,j,k;
    i=i1; j=i2; k=0;
    
    while(i <= j1 && j <= j2){
        if(a[i]<a[j])
            temp[k++] = a[i++];
        else
            temp[k++] = a[j++];
    }
    
    while(i <= j1) 
        temp[k++] = a[i++];
    
    while(j <= j2) 
        temp[k++] = a[j++];
    
    for(i = i1, j = 0; i <= j2; i++,j++)
        a[i]=temp[j];
}
```



## Quick Sort

Quick sort is based on the divide-and-conquer approach based on the idea of choosing one element as a pivot element and partitioning the array around it such that: Left side of pivot contains all the elements that are less than the pivot element Right side contains all elements greater than the pivot

It reduces the space complexity and removes the use of the auxiliary array that is used in merge sort. Selecting a random pivot in an array results in an improved time complexity in most of the cases.

**Input Format**

The first line contains a single integers N denoting the size of the array. The next line contains N space separated integers denoting the contents of the array.

**Constraints**

1<=N<=10^6 1<=A[I]<=10^9

**Output Format**

Print N space separated integers, i.e. the final sorted array.

**Sample Input 0**

```
5
4 3 1 5 2
```

**Sample Output 0**

```
1 2 3 4 5
```

#### Source Code

```C
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

void swap(int *a, int *b){
         int temp = *a;
         *a = *b;
         *b = temp;
}

int partition(int *arr, int low, int high){
    int pivot = arr[high];
    
    int i = (low - 1);
    
    for(int j = low; j < high; j++){
        if(arr[j] <= pivot){
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i+1], &arr[high]);
    return i+1;
}

void quickSort(int *arr, int low, int high){
    if(low < high){
        int pi = partition(arr, low, high);
    quickSort(arr, low, pi - 1);
    quickSort(arr, pi + 1, high);
    }
}

int main() {
    int n, i;
    scanf("%d",&n);
    
    int arr[1000000];
    
    for(i = 0; i < n; i++){
        scanf("%d",&arr[i]);
    }
    
    quickSort(arr, 0, n-1);
    
    for(i = 0; i < n-1; i++){
        printf("%d ",arr[i]);
    }
    
    printf("%d",arr[i]);
    
    return 0;
}

```



## Heap Sort

Heaps can be used in sorting an array. In max-heaps, maximum element will always be at the root. Heap Sort uses this property of heap to sort the array.

**Input Format**

Array is in unsorted manner

**Constraints**

1<=T<10^5 1<=X<=10^6

**Output Format**

Output will come in a sorted manner

**Sample Input 0**

```
5
4
3
2
1
```

**Sample Output 0**

```
1 2 3 4 5
```

#### Source Code

```c
// Heap Sort in C
  
  #include <stdio.h>
  
  // Function to swap the the position of two elements
  void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
  }
  
  void heapify(int arr[], int n, int i) {
    // Find largest among root, left child and right child
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
  
    if (left < n && arr[left] > arr[largest])
      largest = left;
  
    if (right < n && arr[right] > arr[largest])
      largest = right;
  
    // Swap and continue heapifying if root is not largest
    if (largest != i) {
      swap(&arr[i], &arr[largest]);
      heapify(arr, n, largest);
    }
  }
  
  // Main function to do heap sort
  void heapSort(int arr[], int n) {
    // Build max heap
    for (int i = n / 2 - 1; i >= 0; i--)
      heapify(arr, n, i);
  
    // Heap sort
    for (int i = n - 1; i >= 0; i--) {
      swap(&arr[0], &arr[i]);
  
      // Heapify root element to get highest element at root again
      heapify(arr, i, 0);
    }
  }
  
  // Print an array
  void printArray(int arr[], int n) {
    for (int i = 0; i < n; ++i)
      printf("%d ", arr[i]);
    printf("\n");
  }
  
  // Driver code
  int main() {
    int arr[] = {1,2,3,4,5 };
    int n = sizeof(arr) / sizeof(arr[0]);
  
    heapSort(arr, n);
  
   
    printArray(arr, n);
  }
```

