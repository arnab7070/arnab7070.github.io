---
title: 4. Circular Queue Operations 
image: CQueue.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Simplest solution to implement all operations of Circular Queue.
---
## Benifits of Circular Queue 
A circular queue is a type of queue in which the last position is connected to the first position, so that the queue can be treated as a circular list. One benefit of using a circular queue is that it can be implemented using a fixed-size array, which can be more memory efficient than using a dynamic array or a linked list to implement a standard queue.

Since a circular queue uses a fixed-size array, it has a fixed capacity that cannot be changed after the queue is created. This can be an advantage in situations where the size of the queue is known in advance and does not need to change.

Another benefit of a circular queue is that it can be implemented with a single pointer, which points to the front element of the queue. This can be more efficient than using two pointers (one for the front and one for the back) to implement a standard queue.

Overall, the main benefit of using a circular queue is that it can be more memory efficient and potentially faster than a standard queue, depending on the implementation. However, it is important to carefully consider the trade-offs involved and choose the appropriate data structure based on the specific requirements of the application.

> We are now going to see different kind of operations in Circular Queue. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
#define SIZE 6 //Main Size + 1 -> as per my algorithm
using namespace std;
int front = 0, rear = 0;
bool isFull(){
	return (rear+1)%SIZE==front;
}
bool isEmpty(){
	return front==rear;
}
void enque(int arr[], int element){
	if(isFull()){
		cout<<"Error: Queue Overflow!!"<<endl;
		return;
	}
	//It is for circular repeatation
	rear = (rear+1)%SIZE;
	arr[rear] = element;
	cout<<"Pushed element: "<<element<<endl;
}
void deque(int arr[]){
	if(isEmpty()){
		cout<<"Error: Queue Underflow!!"<<endl;
		return;
	}
	front = (front+1)%SIZE;
	cout<<"Popped element: "<<arr[front]<<endl;
}
void peek(int arr[]){
	if(isEmpty()){
		cout<<"Error: Queue Underflow!!"<<endl;
		return;
	}
	cout<<"Front element: "<<arr[(rear+1)%SIZE]<<endl;
}
void display(int arr[]){
	if(isEmpty()){
		cout<<"Error: Queue Underflow!!"<<endl;
		return;
	}
	for(int i = front; i != rear; i=(i+1)%SIZE){
		cout<<arr[(i+1)%SIZE]<<" ";
	}
	cout<<endl;
}
int main() {
  	int arr[SIZE];
	enque(arr, 4);
	enque(arr, 5);
	enque(arr, 6);
	enque(arr, 7);
	enque(arr, 100);
	display(arr);
	enque(arr, 8); //Overflow Condition
	deque(arr); // 4 
	deque(arr); //
	display(arr);
	deque(arr); //6
	deque(arr); //7
	deque(arr); //100
	cout<<isEmpty()<<endl; //1 (True)
	deque(arr); //Underflow Condition
	enque(arr, 10);
	enque(arr, 12);
	display(arr);
	return 0;
}
```
### Output
```
Pushed element: 4
Pushed element: 5
Pushed element: 6
Pushed element: 7
Pushed element: 100
4 5 6 7 100 
Error: Queue Overflow!!
Popped element: 4
Popped element: 5
6 7 100 
Popped element: 6
Popped element: 7
Popped element: 100
1
Error: Queue Underflow!!
Pushed element: 10
Pushed element: 12
10 12
```
