---
title: "Move to Front"
date: 2022-10-16T18:02:11+05:30
draft: false
tags: ["POTD","GFG"]
description: You are given the head of a Linked List. You have to move the last element to the front of the Linked List and return the list.
image: POTD.png
---
# Question
---
You are given the head of a Linked List. You have to move the last element to the front of the Linked List and return the list.
# Example
---
##### Input:
```
N = 5
List = {2,5,6,2,1}
```
##### Output:
```
{1,2,5,6,2}
```
##### Explanation:
In the given linked list, the last element is `1`, after `moving the last element to the front` the linked list will be `{1,2,5,6,2}`.

> Expected Time Complexity: O(N)

> Expected Auxiliary Space: O(1)
# Algorithm
---
We just create a newhead and copy the data of the last node into it. Then we need to point it's next to the main head. We should update the head also to the newhead. Most importantly we should convert the last node to NULL & for the corner case we also create a check for a single node.
# Code
---
```cpp
#include <bits/stdc++.h>
using namespace std;

class ListNode{
public:
    int val;
    ListNode *next;
    ListNode(int x){
        val=x;
        next=NULL;
    }
};

class Solution{
public:
    ListNode *moveToFront(ListNode *head){
        
        //For single node
        if(head->next==NULL){
            return head;
        }
        
        ListNode* temp = head;
        while(temp->next->next!=NULL){
            temp = temp->next;
        }
        ListNode* newhead = new ListNode(temp->next->val);
        newhead->next = head;
        head = newhead; //Updated the head
        temp->next = NULL;

        return head;
    }
};

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        vector<ListNode*> a(n);
        for(int i=0;i<n;i++){
            int x;
            cin>>x;
            a[i]=new ListNode(x);
            if(i!=0){
                a[i-1]->next=a[i];
            }
        }
        ListNode *head=a[0];
        Solution ob;
        head=ob.moveToFront(head);
        while(head!=NULL){
            cout<<head->val;
            if(head->next!=NULL){
                cout<<" ";
            }
            head=head->next;
        }
        cout<<endl;
    }
    return 0;
}
```
# Output
---
```
For Input:
5
2 5 6 2 1
For Output:
1 2 5 6 2
Expected Output:
1 2 5 6 2
```

