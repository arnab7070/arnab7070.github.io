---
title: 2. Stack Operations 
image: Stack.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Want to know more about stack operation check out this blog. 
---
## Some Basic Concepts
A stack is a linear data structure that stores items in a Last-In/First-Out (LIFO) manner. In other words, the last item added to the stack will be the first one to be removed. Some common operations performed on a stack are:

* push: Adds an item to the top of the stack.
* pop: Removes the top item from the stack and returns it.
* peek/top: Returns the top item from the stack without removing it.
* empty: Returns true if the stack is empty, false otherwise.
* full: Returns true if the stack is full, false otherwise.
* size: Returns the total number of elements present in stack. 

### Class of Stack
```cpp
#include <vector>

class Stack {
 public:
  void push(int x) {
    data_.push_back(x);
  }

  int pop() {
    int x = data_.back();
    data_.pop_back();
    return x;
  }

  int top() {
    return data_.back();
  }

  bool empty() {
    return data_.empty();
  }

 private:
  std::vector<int> data_;
};

```

> We are now going to see different kind of operations in `Stack`. So let's get straight into the code. I am using C++ for these operations.
### Code
```cpp
// All stack operations in C++ Easy Implementation
// Operations: [Push,Pop,Peek,Display,IsFull,IsEmpty,Size]
#include <iostream>
#define MAX 5
using namespace std;
int top = -1; // Globally declared variables
bool isFull() { return top == MAX - 1; }
bool isEmpty() { return top == -1; }
void push(int element, int arr[]) {
  if (isFull()) {
    cout << "Error: stack overflow" << endl;
    return;
  }
  top++;
  arr[top] = element;
  cout << "Inserted " << element << endl;
}
void pop(int arr[]) {
  if (isEmpty()) {
    cout << "Error: stack underflow" << endl;
    return;
  }
  cout << "Popped out " << arr[top] << endl;
  top--;
}
void peek(int arr[]) {
  if (isEmpty()) {
    cout << "Error: stack underflow" << endl;
    return;
  }
  cout << "Top element is: " << arr[top] << endl;
}
void size() {
  if (isEmpty()) {
    cout << "Error: stack underflow" << endl;
    return;
  }
  cout << "Size of the stack is: " << top + 1 << endl;
}
void display(int arr[]) {
  if (isEmpty()) {
    cout << "Error: stack underflow" << endl;
    return;
  }
  cout << "Stack elements are as follows: " << endl;
  for (int i = top; i >= 0; i--) {
    cout << arr[i] << endl;
  }
}
int main() {

  int arr[MAX];
  pop(arr);                  // Underflow case
  cout << isEmpty() << endl; // 1 (Yes)
  push(516, arr);
  push(226, arr);
  cout << isEmpty() << endl; // 0 (No)
  cout << isFull() << endl;  // 0 (No)
  push(245, arr);
  push(147, arr);
  push(192, arr);
  push(221, arr);           // Overflow case
  cout << isFull() << endl; // 1 (Yes)
  display(arr);
  pop(arr);  // 192 is the top-most value so it should pop first
  size();    // 5-1 = 4
  peek(arr); // 147 is now top-most value so it should return
}
```
### Output
```
Error: stack underflow
1
Inserted 516
Inserted 226
0
0
Inserted 245
Inserted 147
Inserted 192
Error: stack overflow
1
Stack elements are as follows: 
192
147
245
226
516
Popped out 192
Size of the stack is: 4
Top element is: 147
```
