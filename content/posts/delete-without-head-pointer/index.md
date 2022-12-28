---
title: "Delete Without Head Pointer"
date: 2022-10-13T17:42:04+05:30
draft: false
image: DSA.png
tags: ["Practice Question","GFG","SDE Sheet"]
description: You are given a pointer/ reference to the node which is to be deleted from the linked list of N nodes. The task is to delete the node. Pointer/ reference to head node is not given. 
---
# Question
You are given a pointer/ reference to the node which is `to be deleted` from the linked list of `N` nodes. The task is to delete the node. `Pointer/ reference to head` node is `not` given. 
# Examples
```
Input:
N = 4
value[] = {10,20,4,30}
node = 20
Output: 10 4 30
Explanation: After deleting 20 from
the linked list, we have remaining
nodes as 10, 4 and 30.
```
> Expected Time Complexity : O(1)

> Expected Auxilliary Space : O(1)

# Algorithm
---
We just need to change the data of the given to be deleted node & then we should point it's next pointer to the next of next pointer. We are doing this to skip the copied data node.

---

# Code
```cpp
#include<bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node {
  int data;
  struct Node *next;
  Node(int x) {
    data = x;
    next = NULL;
  }
}*head;

Node *findNode(Node* head, int search_for)
{
    Node* current = head;
    while (current != NULL)
    {
        if (current->data == search_for)
            break;
        current = current->next;
    }
    return current;
}


void insert()
{
    int n,i,value;
    Node *temp;
    scanf("%d",&n);

    for(i=0; i<n; i++)
    {
        scanf("%d",&value);
        if(i==0)
        {
            head=new Node(value);
            temp=head;
            continue;
        }
        else
        {
            temp->next= new Node(value);
            temp=temp->next;
            temp->next=NULL;
        }
    }
}

/* Function to print linked list */
void printList(Node *node)
{
    while (node != NULL)
    {
        printf("%d ", node->data);
        node = node->next;
    }
    cout << endl;
}


class Solution
{
    public:
    //Function to delete a node without any reference to head pointer.
    void deleteNode(Node *del)
    {
        del->data = del->next->data;
        del->next = del->next->next;
    }

};


int main(void)
{
    /* Start with the empty list */

    int t,k,n,value;
    
    scanf("%d",&t);
    while(t--)
    {
        insert();
        scanf("%d",&k);
        Node *del = findNode(head, k);
        Solution ob;
        if (del != NULL && del->next != NULL)
        {
            ob.deleteNode(del);
        }
        printList(head);
    }
    return(0);
}

```

# Output
```
For input:
4
10 20 4 30
20
For output:
10 4 30
Expected output:
10 4 30
```
# Company tags
* `Amazon`
* `Goldman Sachs`
* `Microsoft`
* `Samsung`
* `Visa`