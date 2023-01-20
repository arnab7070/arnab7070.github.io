---
title: Stack Using Linked List
image: StackLL.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Instead of using array we can also use Linked List to implement Stack Operations. Let's see How?? 
---
## Some Basic Concepts
To implement a stack using a linked list, you will need to follow these steps:

1. Define a node data structure that has two fields:
* data: Stores the data for the current node.
* next: Stores a pointer to the next node in the linked list.
2. Define a stack class that has a head field to keep track of the top of the stack.
3. Implement a push function that creates a new node with the given data and updates the head field to point to the new node.
4. Implement a pop function that removes the top item from the stack and returns it. This function should update the head field to point to the next node and delete the old head node.
5. Implement a top function that returns the top item from the stack without removing it.
6. Implement an empty function that returns true if the stack is empty, false otherwise.

> We are now going to see different kind of operations in Stack using Linked List. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
#include <climits>
using namespace std;
class Node{
	public:
	int data;
	Node* next;

	Node(int data){
		this->data = data;
		this->next = NULL;
	}
};

//It is nothing but insert at begin operation in linked list
void push(Node* &top, int data){
	if(top==NULL){
		top = new Node(data);
		return;
	}
	Node* new_node = new Node(data);
	new_node->next = top;
	top = new_node;
}
//It is just a display function of linked list 
void display(Node* top){
	while(top!=NULL){
		cout<<top->data<<" "<<endl;
		top = top->next;
	}
}
//It is nothing but delete at begin function in the linked list
void pop(Node* &top){
	if(top==NULL){
		cout<<"Error: Stack Underflow!!"<<endl;
		return;
	}
	Node* toBeDeleted = top;
	top = top->next;
	cout<<"Deleted "<<toBeDeleted->data<<" successfully."<<endl;
	delete toBeDeleted;
}
//It returns the top value
int peek(Node* &top){
	if(top==NULL){
		cout<<"Error: Stack Underflow!!"<<endl;
		return INT_MIN;
	}
	return top->data;
}
int main() {
	Node* top = NULL;
	push(top, 6);
	push(top, 7);
	push(top, 8);
	display(top);
	pop(top);
	display(top);
	cout<<"Top element is:  "<<peek(top)<<endl;
	pop(top);
	pop(top);
	pop(top); //Error condition
  	return 0;
}
```
### Output
```
8 
7 
6 
Deleted 8 successfully.
7 
6 
Top element is:  7
Deleted 7 successfully.
Deleted 6 successfully.
Error: Stack Underflow!!
```
