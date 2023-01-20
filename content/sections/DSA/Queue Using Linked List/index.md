---
title: Queue Using Linked List 
image: QueueLL.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: We can also implement Queue with the help of Linked List. Check out this blog to know more.
---
## Some Basic Concepts
A queue is a linear data structure that stores items in a First-In/First-Out (FIFO) manner. In other words, the first item added to the queue will be the first one to be removed. To implement a queue using a linked list, you will need to follow these steps:

1. Define a node data structure that has two fields:
* data: Stores the data for the current node.
* next: Stores a pointer to the next node in the linked list.
2. Define a queue class that has two fields:
* head: Keeps track of the front of the queue.
* tail: Keeps track of the back of the queue.
3. Implement an enqueue function that creates a new node with the given data and adds it to the back of the queue. This function should update the tail field to point to the new node.
4. Implement a dequeue function that removes the front item from the queue and returns it. This function should update the head field to point to the next node and delete the old head node.
5. Implement a front function that returns the front item from the queue without removing it.
6. Implement an empty function that returns true if the queue is empty, false otherwise.

> We are now going to see different kind of operations in Queue using Linked List. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
#include <climits>
using namespace std;
class Node{
	public:
	int data;
	Node* next;
	
	//Constructor
	Node(int data){
		this->data = data;
		this->next = NULL;
	}
};
void enque(Node* &front, Node* &rear, int data){
	if(front==NULL && rear==NULL){
		front = new Node(data);
		rear = front;
		return;
	}
	Node* new_node = new Node(data);
	rear->next = new_node;
	rear = new_node;
}
void display(Node* front){
	while(front != NULL){
		cout<<front->data<<" ";
		front = front->next;
	}
	cout<<endl;
}
int temp = INT_MIN; // to store the last value
void deque(Node* &front, Node* &rear){
	if(front==rear){
		if(temp != INT_MIN){
			cout<<"Deleted: "<<temp<<endl;
			temp = INT_MIN;
			return;
		}
		cout<<"Error: Queue is empty"<<endl;
		return;
	}
	if(front->next->next == NULL){
		temp = front->next->data;
	}
	Node* nodeToDelete = front;
	cout<<"Deleted: "<<nodeToDelete->data<<endl;
	front = front->next;
	delete nodeToDelete;
}
int peek(Node* &front, Node* &rear){
	if(front==rear){
		cout<<"Error: Queue is empty"<<endl;
		return INT_MIN;
	}
	return front->data;
}
int main() {
  Node* front = NULL;
  Node* rear = NULL;
	enque(front,rear,5);
	enque(front,rear,1);
	enque(front,rear,9);
	enque(front,rear,7);
	display(front);
	deque(front,rear);
	deque(front,rear);
	cout<<"Top element is: "<<peek(front,rear)<<endl;
	deque(front,rear);
	display(front);
	deque(front,rear);
	deque(front,rear); //Error condition
}
```
### Output
```
5 1 9 7 
Deleted: 5
Deleted: 1
Top element is: 9
Deleted: 9
7 
Deleted: 7
Error: Queue is empty
```
