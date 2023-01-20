---
title: 3. Queue Operations 
image: Queue.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Do you think Queue operations are hard to implement? Don't worry it's so simple. Check out this blog. 
---
## Some Basic Concepts
A queue is a linear data structure that follows the First In, First Out (FIFO) principle. In other words, the first element added to the queue will be the first one to be removed.

Here are some common operations that can be performed on a queue in C++:

* push() or enqueue(): This function is used to insert an element at the end of the queue.

* pop() or dequeue(): This function is used to remove the first element from the queue.

* front(): This function returns the value of the first element in the queue.

* back(): This function returns the value of the last element in the queue.

* empty(): This function returns a boolean value indicating whether the queue is empty or not.

> We are now going to see different kind of operations in Queue. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
#define MAX 5
using namespace std;
int front = -1; // Globally declared variable to keep track of first element
int rear = -1;  // Globally declared variable to keep track of last element

bool isFull() { return rear == MAX - 1; }
bool isEmpty() { return front == rear; }
void enque(int arr[], int element) {
  if (isFull()) {
    cout << "Error: queue full condition" << endl;
    return;
  }
  if (isEmpty() && front == -1) {
    front++; // for the first element it should increase
  }
  rear++;
  cout << "Inserted: " << element << endl;
  arr[rear] = element;
}
void peek(int arr[]) {
  if (isEmpty()) {
    cout << "Error: queue is empty" << endl;
    return;
  }
  cout << "Front element is: " << arr[front] << endl;
}
void deque(int arr[]) {
  if (isEmpty()) {
    cout << "Error: queue is empty" << endl;
    front++; // This is important
    return;
  }
  // For queue FIFO (First In First Out)
  cout << "Popped out successfully" << endl;
  front++;
}
void display(int arr[]) {
  if (isEmpty()) {
    cout << "Error: No element present in Queue" << endl;
    return;
  }
  for (int i = front; i <= rear; i++) {
    cout << arr[i] << "==>";
  }
  cout << "END" << endl;
}
int main() {
  // Main driver code to implement all operations of Queue. I hope it is clear
  // to all of you. You can change the main function as per your own
  // preferences. You can use switch-case menu-driven code for better
  // implementation. Thank You.
  int arr[MAX];

  // Testcase #1:
  // enque(arr, 1);
  // enque(arr, 2);
  // enque(arr, 3);
  // display(arr);
  // deque(arr);
  // deque(arr);
  // deque(arr);
  // enque(arr, 12);
  // enque(arr, 14);
  // enque(arr, 16); // Overflow condition
  // display(arr);
  // peek(arr);
  // deque(arr);
  // deque(arr);
  // display(arr);

  // Testcase #2:
  cout << isEmpty() << endl;
  cout << isFull() << endl;
  enque(arr, 5);
  enque(arr, 4);
  enque(arr, 3);
  enque(arr, 2);
  enque(arr, 1);
  display(arr);  // 5==>4==>3==>2==>1==>END
  enque(arr, 0); // Overflow condition
  peek(arr);     // 5 beacause it was inserted first
  deque(arr);
  deque(arr);
  deque(arr);
  display(arr); // 2==>1==>END
  deque(arr);
  deque(arr);
  display(arr); // END
  deque(arr);   // Underflow condition
}
```
### Output
```
1
0
Inserted: 5
Inserted: 4
Inserted: 3
Inserted: 2
Inserted: 1
5==>4==>3==>2==>1==>END
Error: queue full condition
Front element is: 5
Popped out successfully
Popped out successfully
Popped out successfully
2==>1==>END
Popped out successfully
Error: queue is empty
END
Popped out successfully
```
