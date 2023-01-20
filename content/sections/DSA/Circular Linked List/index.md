---
title: 7. Circular Linked List
image: Circular.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: In this blog we will discuss about different operations of Circular Linked List.
---
## Some Basic Concepts
A circular linked list is a variation of a linked list in which the last node is connected to the first node, forming a circular list. Each node in a circular linked list contains a value and pointers to the previous and next nodes in the list.

There are many operations that can be performed on a circular linked list, such as inserting and deleting nodes, searching for a particular value, and reversing the list.

One advantage of using a circular linked list is that it allows for efficient insertion and deletion at any position in the list, as each node has pointers to both the previous and next nodes. This is similar to a doubly linked list.

Another advantage of a circular linked list is that it can be used to implement a queue or a stack, as the head node can be treated as the front or back of the queue/stack, respectively.

However, it is important to note that circular linked lists require more memory than singly linked lists, as each node requires two pointers instead of one. Therefore, it is important to carefully consider the trade-offs involved and choose the appropriate data structure based on the specific requirements of the application.


> We are now going to see different kind of operations in Circular Linked List. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
// Let's see how to implement different operations of circular linked list
#include <iostream>
using namespace std;
// we are creating a node class to create node of linked list
class Node {
public:
  int data;   // stores the data
  Node *next; // next pointer
  Node *prev; // previous pointer
  // Constructor
  Node(int data) {
    this->data = data;
    this->next = NULL; // initializing next & prev pointer as NULL
    this->prev = NULL;
  }
};
// Insert At Head Function
void insertAtHead(Node *&head, int data) {
  // Corner Case if head == null
  if (head == NULL) {
    head = new Node(data);
    head->next = head;
    head->prev = head->next;
    return;
  }
  // creating new node to connect
  Node *new_node = new Node(data);
  Node *copyHead = head; // copy pointer of head
  while (copyHead->next != head) {
    copyHead = copyHead->next;
  }
  // now copyHead is at last node
  // just link the following nodes as you visualize
  copyHead->next = new_node;
  new_node->prev = copyHead;
  new_node->next = head;
  head->prev = new_node;
  // Updating the head pointer
  head = new_node;
}
// Insert At Tail Function
void insertAtTail(Node *&head, int data) {
  if (head == NULL) {
    insertAtHead(head, data);
    return;
  }
  Node *temp = head; // creating a temp pointer that points to head
  while (temp->next != head) {
    temp = temp->next;
  }
  // Now temp pointer is at last node
  Node *new_node = new Node(data);
  // just link the following nodes with your visualization
  temp->next = new_node;
  new_node->prev = temp;
  new_node->next = head;
  head->prev = new_node;
}
// Delete At Begin Function
void deleteAtBegin(Node *&head) {
  // corner case if there is no element present in the list
  if (head == NULL) {
    cout << "No element is present to delete" << endl;
    return;
  }
  // now to delete from the begin we need to change the linkages
  Node *deleteThisNode = head; // pointer to the head
  deleteThisNode->next->prev = deleteThisNode->prev;
  head->prev->next = head->next;
  head = head->next;
  // delete the node to free it from memory
  delete deleteThisNode;
}
// Delete At End Function
void deleteAtEnd(Node *&head) {
  // Corner Case
  if (head == NULL) {
    deleteAtBegin(head);
    return;
  }
  // new head pointer
  Node *temp = head;
  // Until we reach to the last node we need to traverse
  while (temp->next != head) {
    temp = temp->next;
  }
  // now temp pointer is at last node
  temp->prev->next = temp->next;
  temp->next->prev = temp->prev;
  // delete the temp pointer to free it from memory
  delete temp;
}
void display(Node *head) {
  cout << head->data << "->";
  Node *copyHead = head;
  while (copyHead->next != head) {
    copyHead = copyHead->next;
    cout << copyHead->data << "->";
  }
  // to verify it that it is actually circularly attached
  cout << copyHead->next->data << "(REPEAT)" << endl;
}
int main() {
	//Main driver code to implement the whole thing
	// You can use your own testcases 
	// You can also make it menu driven program if you want
	// For make it simple I call the functions directly
  Node *head = NULL;
  insertAtHead(head, 4); // 4
  insertAtHead(head, 3); // 3->4
  insertAtHead(head, 2); // 2->3->4
  insertAtHead(head, 1); // 1->2->3->4
  insertAtTail(head, 5); // 1->2->3->4->5
  insertAtTail(head, 6); // 1->2->3->4->5->6
  display(head);
  deleteAtBegin(head); // 2->3->4->5->6
  display(head);
  deleteAtEnd(head); // 2->3->4->5
  display(head);
  return 0;
}
```
### Output
```
1->2->3->4->5->6->1(REPEAT)
2->3->4->5->6->2(REPEAT)
2->3->4->5->2(REPEAT)
```
