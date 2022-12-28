---
title: Menu Driven Program For Doubly Linked List
date: 2022-09-17
tags: [DSA, C++, Linked List]
image: featured.jpg
description: Write a menu driven program in C++ to perform the following operations on double linked list.
---

# Question
> Write a menu driven program in C++ to perform the following operations on double linked list.
> 1. insert a node at the beginning of the list.
> 2. insert a node at the end of the list.
> 3. delete a node from the beginning of the list.
> 4. delete a node at the end of the list.
> 5. display the whole list.
---
# Code
```cpp
#include<iostream>
using namespace std;
class node{
	public:
	int data;
	node* prev;
	node* next;
	
	node(int data){
		this->data = data;
		this->prev = NULL;
		this->next = NULL;
	}
};
node* head = NULL;
node* tail = head;
void display(node* &head){
	node* temp = head;
	while(temp != NULL){
		cout<<temp->data<<"->";
		temp = temp->next;
	}
	cout<<"NULL"<<endl;
}

void displayReverse(node* &tail){
	node* temp = tail;
	while(temp != NULL){
		cout<<temp->data<<"->";
		temp = temp->prev;
	}
	cout<<"NULL"<<endl;
}
void insertAtBegin(node* &head, int val){
	if(head==NULL){
		node *temp = new node(val);
		head = temp;
		tail = temp;
		return;
	}
	node* temp = new node(val);
	temp->next = head;
	head->prev = temp;
	head = temp;
}

void insertAtEnd(node* &head, int val){
	if(head == NULL){
		insertAtBegin(head,val);
		return;
	}
	node* temp = head;
	while(temp->next != NULL){
		temp = temp->next;
	}
	temp->next = new node(val);
	temp->next->prev = temp;
	tail = temp->next;
}
void deleteBegin(node* &head){
	if(head==NULL){
		cout<<"No elements present in the linked list to delete"<<endl;
		return;
	}
	if(head->next==NULL){
		cout<<"Deleted: "<<head->data<<endl;
		delete head;
		tail = head = NULL;
		return;
	}
	node* temp = head;
	cout<<"Deleted: "<<temp->data<<endl;
	head->next->prev = NULL;
	head = head->next;
	delete temp;
}
void deleteEnd(node* &head){
	if(head==NULL){
		cout<<"No elements present in the linked list to delete"<<endl;
		return;
	}
	if(head->next==NULL){
		cout<<"Deleted: "<<head->data<<endl;
		delete head;
		tail = head = NULL;
		return;
	}
	node* temp = head;
	while(temp->next!=NULL){
        temp = temp->next;
    }
	cout<<"Deleted: "<<temp->data<<endl;
    temp->prev->next = NULL;
	delete temp;
}
int main(){
	node* head = NULL;
	system("clear");
	int x;
	cout<<"1 -> Insert Begin\n2 -> Insert End\n3 -> Delete Begin\n4 -> Delete End\n5 -> Display\n6 -> Reverse Display\n7 -> For Quit"<<endl;
	while(x != 7){
		cout<<"Enter any option: ";
		cin>>x;
		switch(x){
			//Insert Begin
			case 1:
				int val;
				cout<<"Enter an element: ";
				cin>>val;
				insertAtBegin(head,val);
				break;
		   //Insert End
			case 2:
				int item;
				cout<<"Enter an element: ";
				cin>>item;
				insertAtEnd(head,item);
				break;
			//Delete Begin
			case 3:
			    deleteBegin(head);
				break;
			//Delete End
			case 4:
                deleteEnd(head);
				break;
			//Display
			case 5:
				display(head);
				break;
			case 6:
				displayReverse(tail);
				break;
			//Reverse Display
			case 7:
				cout<<"Thanks for using Doubly Linked List"<<endl;
				break;	
		}
	}
	return 0;
}
```
```cpp
Output
1 -> Insert Begin
2 -> Insert End
3 -> Delete Begin
4 -> Delete End
5 -> Display
6 -> Reverse Display
7 -> For Quit
Enter any option: 1
Enter an element: 10
Enter any option: 2
Enter an element: 15
Enter any option: 1
Enter an element: 5
Enter any option: 2
Enter an element: 20
Enter any option: 5
5->10->15->20->NULL
Enter any option: 6
20->15->10->5->NULL
Enter any option: 3
Deleted: 5
Enter any option: 4
Deleted: 20
Enter any option: 5
10->15->NULL
Enter any option: 7
Thanks for using Doubly Linked List
```