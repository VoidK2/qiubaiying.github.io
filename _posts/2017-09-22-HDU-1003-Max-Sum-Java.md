---
layout:     post
title:      HDU 1003 Max Sum 三种解法
subtitle:   HDU 1003 JAVA dp
date:       2017-09-22
author:     zhangzexin
header-img: img/post-bg-unix-linux.jpg
catalog:    true
tags:
    - HDU
    - Java
    - dp
---


## c++ dp 46ms
```c++
//2
//5 6 -1 5 4 -7
//7 0 6 -1 1 -6 7 -5
//Case 1:
//14 1 4

//Case 2:
//7 1 6
#include <cstdio>  
#include <cstring>
using namespace std;  
int main(){
	int ncase,n;
	int dp[100100];
	scanf("%d",&ncase);
	for(int k=1;k<=ncase;k++){
		scanf("%d",&n);
		int last=1,first=1,temp=1,maxsum=-1001,sum=0;
		memset(dp,0,sizeof(dp));
		for(int i=1;i<=n;i++){
			scanf("%d",&dp[i]);
		    sum=0;
			//maxsum=dp[1];
		}
		for(int i=1;i<=n;i++){
			sum+=dp[i];
			if(sum>maxsum){
				maxsum=sum;
				first=temp;
				last=i;
			}
			if(sum<0){
				sum=0;
				temp=i+1;
			}
		}
		printf("Case %d:\n%d %d %d\n",k,maxsum,first,last);
		if (k<ncase)  
        {  
            printf("\n");  
        }
	}
}

```


## c++ 暴力 86ms
```c++
#include <iostream>  
using namespace std;  
int main()  
{  
    int j,i,k,n,m,t;  
    int a;  
    scanf("%d",&t);  
    for (j=1;j<=t;j++)  
    {  
        scanf("%d",&n);  
        int sum=0,maxsum=-1001,first =0, last = 0, temp = 1;  
        for (i=0;i<n;i++)  
        {  
            scanf("%d",&a); 
            sum += a;  
            if (sum > maxsum)  
            {  
                maxsum = sum;first = temp;last = i+1;  
            }  
            if (sum < 0)  
            {  
                sum = 0;temp = i+2;  
            }  
        }  
        printf("Case %d:\n%d %d %d\n",j,maxsum,first,last);  
        if (j!=t)  
        {  
            printf("\n");  
        }  
    }  
      
    return 0;  
}
```


## java 暴力 608ms
```java

import java.util.Scanner;
public class Main{
	public static void main(String[] args){
		int _case,n,i;
		int []a=new int [100100];
		int []b=new int [100100];
		int []c=new int [100100];
			Scanner in=new Scanner(System.in);
			_case=in.nextInt();
			int js=0;
			while(_case-->0){
				js++;
				n=in.nextInt();
				for(i=0;i<n;i++){
					a[i]=in.nextInt();
				}
				b[0]=a[0];
				c[0]=0;
				for(i=1;i<n;i++){
					if(b[i-1]+a[i]<a[i]){
						b[i]=a[i];
						c[i]=i;
					}
					else{
						b[i]=b[i-1]+a[i];
						c[i]=c[i-1];
					}
				}
				int ed=0;
				int max=b[0];
				for(i=1;i<n;i++){
					if(max<b[i]){
						max=b[i];
						ed=i;
					}
				}
				System.out.println("Case "+js+":");
				System.out.println(max+" "+(c[ed]+1)+" "+(ed+1));
				if(_case>0)
				System.out.println();
			}
	}
}
```
