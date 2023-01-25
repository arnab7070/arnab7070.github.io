---
title: Priority Queue Operations 
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
#include <iostream>
using namespace std;
class Node{
	public:
	int data;
	int priority;
	Node* next;
	Node(int data, int priority){
		this->data = data;
		this->priority = priority;
		this->next = NULL;
	}
};

void insert(Node* &head, int data, int priority){
	Node* newNode = new Node(data, priority);
	if(head == NULL || priority < head->priority){
		newNode->next = head;
		head = newNode;
		return;
	}
	Node *temp = head;
	while(temp->next != NULL && temp->next->priority <= priority){
		temp = temp->next;
	}
	newNode->next = temp->next;
	temp->next = newNode;
	
}
void deleteNode(Node* &head){
	if(head == NULL){
		cout<<"No data present"<<endl;
		return;
	}
	cout<<"Deleted: "<<head->data<<endl;
	Node* temp = head;
	head = head->next;
	delete temp;
	
}
void isEmpty(Node* &head){
	if(head == NULL){
		cout<<"List is empty"<<endl;
		return;
	}
	cout<<"List has some data"<<endl;
}
void display(Node* head){
	while(head!=NULL){
		cout<<head->data<<"@"<<head->priority<<"->";
		head = head->next;
	}
	cout<<"NULL"<<endl;
}

int main(){
	Node* head = NULL;
	isEmpty(head);
	insert(head, 1, 4);
	insert(head, 2, 1);
	insert(head, 5, 3);
	insert(head, 7, 2);
	insert(head, 8, 5);
	display(head);
	deleteNode(head);
	isEmpty(head);
	display(head);
	return 0;
}
```

### Output
```
List is empty
2@1->7@2->5@3->1@4->8@5->NULL
Deleted: 2
List has some data
7@2->5@3->1@4->8@5->NULL
```
