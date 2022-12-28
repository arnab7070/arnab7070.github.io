---
title: "BFS Traversal"
date: 2022-09-23T20:44:48+05:30
tags: [DSA, C++, BFS, Graph]
image: BFS.jpg
description: C++ code to implement BFS Traversal.
draft: false
---
# Code in C++ to perform BFS
---
# Code
```cpp
#include<iostream>
#include<queue>
#include<algorithm>
using namespace std;
int main(){


   queue<int> q;
   int u;
   int i = 0; //here we are starting exploration from 0. 
   //int i = 1; //here we are starting exploration from 1.
   //int i = 2; //here we are starting exploration from 2.
   int visited[7]={0,0,0,0,0,0,0};
   int a[7][7] = {
       {0,1,1,1,0,0,0},                 
       {1,0,1,0,0,0,0}, 
       {1,1,0,1,1,0,0},
       {1,0,1,0,1,0,0},
       {0,0,1,1,0,1,1},
       {0,0,0,0,1,0,0},
       {0,0,0,0,1,0,0},
    };
/*
 ->Graph Structure :
   0 __ 1
   |    |
   3 __ 2   
    \  /
     4
   /   \
  5     6 
*/
    cout<<i<<" ";
    visited[i]=1;
    q.push(i); //enqueue i for exploration
    while(!q.empty()){
        int node = q.front();
        q.pop();
        for(int j = 0; j < 7; j++){
            if(a[node][j] == 1 && visited[j]==0)
            {
                cout<<j<<" ";
                visited[j]=1;
                q.push(j); //enqueue i for exploration
            }
        }
    }

return 0;
}
```
# Output
```cpp
0 1 2 3 4 5 6 
```
