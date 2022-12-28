---
title: "Stack Using Linked List"
date: 2022-10-03T20:51:21+05:30
tags: [DSA, C++, Linked List, Stack]
image: Stack Using Linked List.png
description: C++ code to implement Stack using linked list.
draft: false
---
# Question
> Write a code to implement Stack using Linked List
# Algorithm
> It's so simple to implement because stack uses LIFO and thats why we use insertAtBegin function only for inserting elements.
> And to delete elements we just need to implement delete from the end function
# Code
---
```cpp
#include <iostream>
using namespace std;
//Node structure for building stack
class node{
	public:
	int data;
	node* next;
	
	//Constructor
	node(int data){
		this->data = data;
		this->next = NULL;
	}	
	
};
//First In Last Out Method (F-I-L-O Method)
void insertAtBegin(node* &head, int data){
	node* temp = new node(data);
	cout<<"Pushed: "<<data<<endl;
	if(head==NULL){
		head = temp;
		return;
	}
	
	temp->next = head;
	head = temp;
}
//Display fuction to display the whole list
void display(node* head){
	if(head==NULL){
		cout<<"Stack Underflow"<<endl;
		return;
	}
	while(head!=NULL){
		cout<<head->data<<"->";
		head = head->next;
	}
	cout<<"NULL"<<endl;
}
//Removing element from the last of the list
void deleteAtEnd(node* &head){
	
	if(head==NULL){
		cout<<"Stack Underflow"<<endl;
		return;
	}
	
	cout<<"Popped: "<<head->data<<endl;
	node* temp = head;
	head = head->next;
	delete temp;
	
}
		                  
int main(){
	
	node* head = NULL;
	while(true){
		cout<<"1. Push\n2. Pop\n3. Display\n0. Exit\n";
		int option;
		cout<<"Enter any option: ";
		cin>>option;
		
		switch(option){
			case 1:
				int element;
				cout<<"Enter the element to be pushed into stack: ";
				cin>>element;
				insertAtBegin(head,element);
				break;
			case 2:
				deleteAtEnd(head);
				break;
			case 3:
				display(head);
				break;
			default:
				cout<<"Thanks for using stack using Linked List"<<endl;
				return 0;
		}
	}
	return 0;
}
```
# Output
```cpp
1. Push
2. Pop
3. Display
0. Exit
Enter any option: 1
Enter the element to be pushed into stack: 10
Pushed: 10
Enter any option: 1
Enter the element to be pushed into stack: 20
Pushed: 20
Enter any option: 1
Enter the element to be pushed into stack: 30
Pushed: 30
Enter any option: 1
Enter the element to be pushed into stack: 40
Pushed: 40
Enter any option: 3
40->30->20->10->NULL
Enter any option: 2
Popped: 40
Enter any option: 2
Popped: 30
Enter any option: 3
20->10->NULL
Enter any option: 0
Thanks for using stack using Linked List
```