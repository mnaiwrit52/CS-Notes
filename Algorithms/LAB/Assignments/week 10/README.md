# DAA Week 10 (Practise Set)

## Counting Pretty Numbers

Vasya likes the number 239. Therefore, he considers a number pretty if its last digit is 2, 3 or 9.

Vasya wants to watch the numbers between L and R (both inclusive), so he asked you to determine how many pretty numbers are in this range. Can you help him?

**Input Format**

Input • The first line of the input contains a single integer T denoting the number of test cases. The description of T test cases follows. • The first and only line of each test case contains two space-separated integers L and R.

**Constraints**

Constraints • 1≤T≤100 • 1≤L≤R≤10^5

**Output Format**

Output For each test case, print a single line containing one integer — the number of pretty numbers between L and R.

**Sample Input 0**

```
Sample Input 1 
2
1 10
11 33
```

**Sample Output 0**

```
Sample Output 1 
3
8
```

**Explanation 0**

Example case 1: The pretty numbers between 1 and 10 are 2, 3 and 9. Example case 2: The pretty numbers between 11 and 33 are 12, 13, 19, 22, 23, 29, 32 and 33.

#### Source Code

```c++
#include<iostream>
using namespace std;
int main()
{
    int t;
    cin>>t;
    while(t--)
    {
       int array[10][10],l,r,count=0;
    
    cin>>l>>r;
    for(int i=l;i<=r;i++)
    {
        if(i%10==2 ||i%10==3 || i%10==9)
        {
            count++;
        }
    }
    cout<<count<<endl;
    }
    
}
```



## Ciel and Reciept

Tomya is a girl. She loves Chef Ciel very much. Tomya like a positive integer p, and now she wants to get a receipt of Ciel's restaurant whose total price is exactly p. The current menus of Ciel's restaurant are shown the following table.

![image](https://s3.amazonaws.com/hr-assets/0/1650971961-47c3c78240-sample_table.png)

Note that the i-th menu has the price 2i-1 (1 ≤ i ≤ 12). So please find the minimum number of menus whose total price is exactly p. Note that if she orders the same menu twice, then it is considered as two menus are ordered. (See Explanations for details)

**Input Format**

Input The first line contains an integer T, the number of test cases. Then T test cases follow. Each test case contains an integer p. Sample Input 1 4 10 256 255 4096

**Constraints**

Constraints 1 ≤ T ≤ 5 1 ≤ p ≤ 100000 (105) There exist combinations of menus whose total price is exactly p.

**Output Format**

Output For each test case, print the minimum number of menus whose total price is exactly p. Sample Output 1 2 1 8 2 Explanation In the first sample, examples of the menus whose total price is 10 are the following: 1+1+1+1+1+1+1+1+1+1 = 10 (10 menus) 1+1+1+1+1+1+1+1+2 = 10 (9 menus) 2+2+2+2+2 = 10 (5 menus) 2+4+4 = 10 (3 menus) 2+8 = 10 (2 menus) Here the minimum number of menus is 2. In the last sample, the optimal way is 2048+2048=4096 (2 menus). Note that there is no menu whose price is 4096.

**Sample Input 0**

```
Sample Input 1 
4
10
256
255
4096
```

**Sample Output 0**

```
Sample Output 1 
2
1
8
2
```

**Explanation 0**

Explanation In the first sample, examples of the menus whose total price is 10 are the following: 1+1+1+1+1+1+1+1+1+1 = 10 (10 menus) 1+1+1+1+1+1+1+1+2 = 10 (9 menus) 2+2+2+2+2 = 10 (5 menus) 2+4+4 = 10 (3 menus) 2+8 = 10 (2 menus) Here the minimum number of menus is 2. In the last sample, the optimal way is 2048+2048=4096 (2 menus). Note that there is no menu whose price is 4096.

#### Source Code

```c++
#include<stdio.h>
#include<math.h>
int main(){
    int t;
    scanf("%d",&t);
   
    while(t--){
        int p,i,count=0,j;
        scanf("%d",&p);
        while(p>2048){
            count++;
            p-=2048;
        }
        while(p!=0){
   
        for(i=0;i<13;i++){
            if(pow(2,i)>p){
                count++;
                break;   
            }
           
        }
        j=i-1;
        p=p-pow(2,j);
       
    }
        printf("%d\n",count);   
       
    }
    return 0;
}
```

