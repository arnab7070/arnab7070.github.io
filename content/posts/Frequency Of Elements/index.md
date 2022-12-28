---
title: Frequency Of Elements
date: 2022-09-15
tags: [array, DSA, map]
image: notebook.jpg
description: Program to find the frequency of each element of an array
---

# Question
> Q. Program to find the frequency of each element of an array.
---
# Algorithm

- Step 1: Create a map of integer to store key-value pairs. map<int,int>.

- Step 2: Now iterate over all the elements of the array and count their frequency by the help of map.

- Step 3: Now make a iterator for map to iterate over the map items.

- Step 4: This is the final step. Just print all the elements and their frequency stored in map respectively.

# Code
> Here is the C++ implementation of the given problem

```cpp
#include<iostream>
#include<map>
#include<vector>
using namespace std;
int main()
{
    map<int,int> m;
    int n; //Number of elements in array
    cin>>n;
    vector<int> arr(n);
    for(int i = 0; i < n; i++){
        cin>>arr[i];
    }
    for(int x: arr){
        m[x]++; //main line for solving this problem
    }
    map<int, int> :: iterator it;
    for(it = m.begin(); it != m.end(); it++){
        cout<<it->first<<"->"<<it->second<<endl;
    }
    return 0;
}
```
```cpp
Output
10
1 5 2 1 5 3 2 2 5 2
1->2
2->4
3->1
5->3
```
