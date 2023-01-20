---
title: 6. Doubly Linked List 
image: DLL.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Want to know the basic concepts of Doubly Linked List. Check out this blog.
---
## Some Basic Concepts
A doubly linked list is a linear data structure that consists of a sequence of nodes, where each node contains a value and pointers to the previous and next nodes in the list. The first and last nodes have null pointers for their previous and next nodes, respectively, indicating the beginning and end of the list.

#### Structure of Node
```c
struct Node {
  int value;
  Node* prev;
  Node* next;
};
```
There are many operations that can be performed on a doubly linked list, such as inserting and deleting nodes, searching for a particular value, and reversing the list.

One advantage of using a doubly linked list is that it allows for efficient insertion and deletion at any position in the list, as each node has pointers to both the previous and next nodes. In contrast, a singly linked list only allows for efficient insertion and deletion at the head of the list.

Another advantage of a doubly linked list is that it allows for traversal in both directions, as the nodes have pointers to both the previous and next nodes. This can be useful in certain applications where it is necessary to traverse the list backwards as well as forwards.

However, it is important to note that doubly linked lists require more memory than singly linked lists, as each node requires two pointers instead of one. Therefore, it is important to carefully consider the trade-offs involved and choose the appropriate data structure based on the specific requirements of the application.

> We are now going to see different kind of operations in Doubly Linked List. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
using namespace std;
class Node {
public:
  int data;
  Node *next;
  Node *prev;

  // Constructor
  Node(int data) {
    this->data = data;
    this->next = NULL;
    this->prev = NULL;
  }
};

void display(Node *head) {
  while (head != NULL) {
    cout << head->data << "->";
    head = head->next;
  }
  cout << "NULL" << endl;
}
void printReverse(Node *head) {
  // to place the pointer at the last node
  while (head->next != NULL) {
    head = head->next;
  }
  cout << "Printing the list in reverse order: ";
  while (head != NULL) {
    cout << head->data << "->";
    head = head->prev;
  }
  cout << "NULL" << endl;
}
void insertAtHead(Node *&head, int data) {
  if (head == NULL) {
    head = new Node(data);
    return;
  }
  Node *new_head = new Node(data);
  new_head->next = head;
  head->prev = new_head;
  head = new_head;
}
void insertAtTail(Node *&head, int data) {
  if (head == NULL) {
    insertAtHead(head, data);
    return;
  }
  Node *new_tail = new Node(data);
  Node *temp = head;
  while (temp->next != NULL) {
    temp = temp->next;
  }
  temp->next = new_tail;
  new_tail->prev = temp;
}
void deleteAtHead(Node *&head) {
  if (head == NULL) {
    cout << "There is no element to delete" << endl;
    return;
  }
  Node *nodeToBeDeleted = head;
  head = head->next;
  head->prev = NULL;
  delete nodeToBeDeleted;
}
void deleteAtTail(Node *&head) {
  if (head == NULL) {
    cout << "There is no element to delete" << endl;
    return;
  }
  Node *temp = head;
  while (temp->next != NULL) {
    temp = temp->next;
  }
  Node *nodeToBeDeleted = temp; // It is the last node
  // Change the linking of the linked list
  temp->prev->next = NULL;
  delete nodeToBeDeleted;
}
void insertAtIndex(Node *&head, int data, int index) {
  if (head == NULL) {
    insertAtHead(head, data);
    return;
  }
  int currPosition = 0;
  Node *temp = head;
  while (currPosition < index - 1) {
    temp = temp->next;
	  currPosition++;
  }
  Node *new_node = new Node(data);
  // Now linking should be done
  new_node->next = temp->next;
  temp->next->prev = new_node;
  temp->next = new_node;
  new_node->prev = temp;
}
void deleteAtIndex(Node* &head, int index){
	if (head == NULL) {
    deleteAtHead(head);
    return;
  }
  int currPosition = 0;
  Node *temp = head;
  while (currPosition < index) {
    temp = temp->next;
	  currPosition++;
  }
	//We are now at that index which node is to be deleted
	//Now we should change the internal linkings
	temp->next->prev = temp->prev;
	temp->prev->next = temp->next;
	delete temp;
}
int main() {
  Node *head = NULL;
  insertAtHead(head, 1);
  insertAtHead(head, 2);
  insertAtHead(head, 3);
  insertAtHead(head, 4);
  insertAtIndex(head, 10, 3);
  display(head);
  deleteAtIndex(head, 3);
  display(head);
  insertAtTail(head, 5);
  insertAtTail(head, 6);
  display(head);
  deleteAtHead(head);
  deleteAtTail(head);
  display(head);
  printReverse(head);
  return 0;
}
```
### Output
```
4->3->2->10->1->NULL
4->3->2->1->NULL
4->3->2->1->5->6->NULL
3->2->1->5->NULL
Printing the list in reverse order: 5->1->2->3->NULL
```
