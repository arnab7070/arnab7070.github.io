---
title: "Max Min"
date: 2022-10-13T17:10:45+05:30
draft: false
tags: ["GFG","POTD"]
description: Given an array A of size N of integers. Your task is to find the sum of minimum and maximum element in the array.
image: POTD.png
---
# Question
`[Problem of the day 13-10-2022]`

Given an array `A` of size `N` of integers. Your task is to find the sum of `minimum and maximum` element in the array.
# Example
```
Input
N = 5
A[] = {-7, 10, -4, 5, 1}
Output: 3
Explanation: min = -7, max =  10. Sum = -7 + 10 = 3
```
> Expected Time Complexity: O(N)

> Expected Auxiliary Space: O(1)

# Algorithm
---
This is a really simple question of array. You just need to sort the array in ascending order then just return the value of the sum of first & last element of the array.

---
# Code
```cpp
#include<bits/stdc++.h>
using namespace std;

class Solution
{
   public:
    int findSum(int A[], int N)
    {
        //inbuilt function for sorting
    	sort(A,A+N);
    	return A[0]+A[N-1];
    }

};

int main()
{
	int t;
	cin>>t;
	while(t--)
	{
	    int n;
	    cin>>n;
	    int arr[n];
	    for(int i=0;i<n;i++)
	      cin>>arr[i];
	    Solution ob;  
	    int ans=ob.findSum(arr, n);
	    cout<<ans;
	    cout<<"\n";
	}
	return 0;
}

```
# Output
```
For input: 
5
-7 10 -4 5 1
Output:
3
Expected Output:
3
```