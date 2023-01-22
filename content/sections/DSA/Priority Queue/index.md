---
title: Queue Operations 
image: PQueue.gif
date: 2023-01-22
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Here we will cover all about priority queue operations in a single blog. 
---
## Some Basic Concepts
A priority queue is a data structure that stores elements in a specific order based on their priority. Elements with higher priority are served before elements with lower priority. There are two main types of priority queues: max-priority queues, where the element with the highest priority is served first, and min-priority queues, where the element with the lowest priority is served first. Priority queues can be implemented using various data structures, such as an array, a linked list, or a binary heap.


Here are some common operations that can be performed on priority queue in C++:

1. Insertion: This operation adds an element to the queue with a specified priority.
2. Peek/Top: This operation returns the element with the highest or lowest priority (depending on whether it's a max-priority or min-priority queue) without removing it from the queue.
3. Extract/Pop: This operation removes and returns the element with the highest or lowest priority (depending on whether it's a max-priority or min-priority queue).
4. Decrease/Increase Key: This operation modifies the priority of an element already in the queue.
5. Delete: This operation removes a specific element from the queue.

These are just a few examples of the operations that can be performed on priority queue in C++. There are many other operations that can be performed on priority queue, and the specific operations that are available depend on the programming language you are using.

> We are now going to see different kind of operations in Priority Queue. So let's get straight into the code. I am using C++ for these operations.
### Code
```cpp
// Priority Queue Implementation Using Linked List
#include <iostream>
using namespace std;
class Node
{
public:
    int data;
    Node *next;

    // Constructor
    Node(int data)
    {
        this->data = data;
        this->next = NULL;
    }
};

void enque(Node *&head, int item)
{
    // if node == NULL
    if (head == NULL)
    {
        Node *new_node = new Node(item);
        head = new_node;
        return;
    }
    // if single node was there
    else if (head->next == NULL)
    {
        Node *new_node = new Node(item);
        if (item < head->data)
        {
            new_node->next = head;
            head = new_node;
            return;
        }
        head->next = new_node;
        return;
    }
    // Else check the priority for other condition
    Node *temp = head;

    while (temp->next != NULL && item > temp->data && item > temp->next->data)
    {
        // temp->next != NULL it should check first to avoid segmentation fault
        /* item > temp->next->data is for Handling the mid insertion */
        /* temp->next != NULL is for Important for handling tail case */
        temp = temp->next;
    }

    Node *new_node = new Node(item);
    // Handling the tail insert case
    if (temp->next == NULL)
    {
        temp->next = new_node;
        return;
    }
    // Handling the mid insertion case
    new_node->next = temp->next;
    temp->next = new_node;
}
// Plain delete from begin operation in Linked List
void deque(Node *&head)
{
    if (head == NULL)
    {
        cout << "Error: No element present in the priority queue." << endl;
        return;
    }
    Node *temp = head;
    head = head->next;
    delete temp;
}
void display(Node *head)
{
    while (head != NULL)
    {
        cout << head->data << "->";
        head = head->next;
    }
    cout << "NULL" << endl;
}

int main()
{
    Node *head = NULL;
    enque(head, 7);
    enque(head, 1);
    enque(head, 3);
    enque(head, 2);
    enque(head, 10);
    enque(head, 4);
    enque(head, 5);
    enque(head, 4);
    display(head);
    deque(head);
    // deque(head);
    display(head);
    return 0;
}

```
### Output
```
1->2->3->4->4->5->7->10->NULL
2->3->4->4->5->7->10->NULL
```
