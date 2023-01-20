---
title: 5. Linked List Operations 
image: Linked.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Here we will cover all about Linked List operations in a single blog. 
---
## Some Basic Concepts

A singly linked list is a linear data structure that consists of a sequence of nodes, where each node contains a value and a pointer to the next node in the list. The last node in the list points to a null pointer, indicating the end of the list.

#### Structure of a Node
```c
struct Node {
  int value;
  Node* next;
};
```
There are many operations that can be performed on a singly linked list, such as inserting and deleting nodes, searching for a particular value, and reversing the list.

One advantage of using a linked list is that it can be easily resized by adding or removing nodes, as it does not have a fixed size like an array. However, linked lists have slower access times than arrays, as elements must be accessed sequentially starting from the head of the list.

### Operations
There are several common operations that can be performed on a singly linked list:

1. Insertion: Inserting a new node into the list can be done at the head of the list (called "prepending"), at the tail of the list (called "appending"), or at a specific position in the list.

2. Deletion: Deleting a node from the list can be done by deleting the head node, the tail node, or a specific node in the list.

3. Searching: Searching for a particular value in the list can be done by traversing the list and comparing the values of the nodes.

4. Reversing: Reversing the list can be done by iterating through the list and swapping the pointers of the nodes.

5. Sorting: Sorting the list can be done by implementing a sorting algorithm such as bubble sort or merge sort.

> We are now going to see different kind of operations in Linked List. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
#include <stack>
using namespace std;
class Node {
public:
  int data;
  Node *next;

  // Constructor
  Node(int data) {
    this->data = data;
    this->next = NULL;
  }
};

// display function
void displayList(Node *head) {
  while (head != NULL) {
    cout << head->data << "->";
    head = head->next;
  }
  cout << "NULL" << endl;
}
// insert a node at the tail
void insertAtTail(Node *&head, int data) {
  if (head == NULL) {
    head = new Node(data);
    return;
  }
  Node *root = head;
  while (root->next != NULL) {
    root = root->next;
  }
  root->next = new Node(data);
}
// insert a node at head
void insertAtHead(Node *&head, int data) {
  if (head == NULL) {
    head = new Node(data);
    return;
  }
  Node *root = new Node(data);
  root->next = head;
  head = root;
}
void insertAtIndex(Node *&head, int data, int index) {
  if (head == NULL) {
    head = new Node(data);
    return;
  }
  int curr_index = 0;
  Node *root = head;
  while (curr_index < index - 1) {
    root = root->next;
    curr_index++;
  }
  Node *new_node = new Node(data);
  new_node->next = root->next;
  root->next = new_node;
}
void searchNode(Node *head, int data) {
  if (head == NULL) {
    cout << "No element present in the linked list" << endl;
    return;
  }
  while (head != NULL) {
    if (head->data == data) {
      cout << "Element is present" << endl;
      return;
    }
    head = head->next;
  }
  cout << "Element is not present" << endl;
}
void deleteAtFirst(Node *&head) {
  if (head == NULL) {
    cout << "No element present in the linked list" << endl;
    return;
  }
  Node *toBeDeletedNode = head;
  head = head->next;
  delete toBeDeletedNode;
}
void deleteAtTail(Node *&head) {
  if (head == NULL) {
    cout << "No element present in the linked list" << endl;
    return;
  }
  Node *temp = head;
  while (temp->next->next != NULL) {
    temp = temp->next;
  }
  delete temp->next;
  temp->next = NULL;
}
void deleteAtIndex(Node *&head, int index) {
  if (head == NULL) {
    cout << "No element present in the linked list" << endl;
    return;
  }
  int curr_index = 0;
  Node *nodeToBeDeleted = head;
  while (curr_index < index - 1) {
    nodeToBeDeleted = nodeToBeDeleted->next;
    curr_index++;
  }
  // cout<<"Delete: "<<nodeToBeDeleted->next->data<<"\t";

  // Approach 1:
  // Node* nextNode = nodeToBeDeleted->next->next;
  // delete nodeToBeDeleted->next;
  // nodeToBeDeleted->next = nextNode;

  // Approach 2:
  Node *deleteNode = nodeToBeDeleted->next;
  nodeToBeDeleted->next = nodeToBeDeleted->next->next;
  delete deleteNode;
}
Node *reverseLinkedList(Node *head) {
  // Approach 1: Using stack
  // stack<int> st;
  // while(head != NULL){
  // 	st.push(head->data);
  // 	head = head->next;
  // }
  // Node* reversedNode = NULL;
  // while(!st.empty()){
  // 	insertAtTail(reversedNode, st.top());
  // 	st.pop();
  // }
  // return reversedNode;

  // Approach 2: Without using stack
  Node *reversedNode = NULL;
  while (head != NULL) {
    insertAtHead(reversedNode, head->data);
    head = head->next;
  }
  return reversedNode;
}

// If we want to reverse the list itself not want to create another reversed
// list then we should use the following function

void reverseListItself(Node *&head) {
  stack<int> st;
  Node *temp = head;
  while (temp != NULL) {
    st.push(temp->data);
    temp = temp->next;
  }
  temp = head; // re-initialize it with head pointer
  while (temp != NULL) {
    temp->data = st.top();
    st.pop();
    temp = temp->next;
  }
}

void listSize(Node *head) {
  int size = 0;
  while (head != NULL) {
    size++;
    head = head->next;
  }
  cout << "Size of the list is: " << size << endl;
}

Node* recursiveReverse(Node* head){
	if(head==NULL || head->next==NULL){
		return head;
	}
	Node* smallHead =recursiveReverse(head->next);
	head->next->next = head;
	head->next = NULL;
	return smallHead;
}
int main() {
  // Crating an object of Node
  Node *root = NULL;
  searchNode(root, 8);
  insertAtTail(root, 7);
  insertAtTail(root, 8);
  insertAtTail(root, 10);
  displayList(root);
  insertAtHead(root, 5);
  insertAtHead(root, 59);
  insertAtIndex(root, 100, 1);
  displayList(root);
  searchNode(root, 50);
  searchNode(root, 8);
  deleteAtFirst(root);
  displayList(root);
  deleteAtTail(root);
  displayList(root);
  deleteAtIndex(root, 1);
  displayList(root);
  Node *reverseLinkedListNode = reverseLinkedList(root);
  displayList(reverseLinkedListNode);
  reverseListItself(root);
  displayList(root);
  listSize(root);
  Node* recursiveHead = recursiveReverse(root);
  displayList(recursiveHead);
  return 0;
}
```
### Output
```
No element present in the linked list
7->8->10->NULL
59->100->5->7->8->10->NULL
Element is not present
Element is present
100->5->7->8->10->NULL
100->5->7->8->NULL
100->7->8->NULL
8->7->100->NULL
8->7->100->NULL
Size of the list is: 3
100->7->8->NULL
```
