---
title: 1. Array Operations 
image: Array.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Here we will cover all about array operations in a single blog. 
---
## Some Basic Concepts
In C++, an array is a collection of items that are stored in a contiguous block of memory. The items can be of the same type or of different types, and the type of the items is specified when the array is declared.

Here is an example of how to declare and initialize an array of integers in C++:
```cpp
int arr[10]; // Declare an array of 10 integers

int arr[5] = {1, 2, 3, 4, 5}; // Declare and initialize an array of 5 integers

```
Here are some common operations that can be performed on arrays in C++:

1. Accessing an element: You can access a specific element in an array by using its index. For example, if arr is an array of integers, you can access the first element in the array using arr[0].

2. Modifying an element: You can modify an element in an array by assigning a new value to it. For example, if arr is an array of integers and arr[0] is the first element in the array, you can modify the value of arr[0] by assigning a new value to it, like this: arr[0] = 10.

3. Adding an element: C++ does not have a built-in method for adding an element to an array. However, you can implement this functionality yourself by using a separate variable to keep track of the number of elements in the array, and then using a loop to shift the elements of the array one position to the right to make room for the new element.

4. Removing an element: C++ does not have a built-in method for removing an element from an array. However, you can implement this functionality yourself by using a loop to shift the elements of the array one position to the left to fill the gap left by the removed element.

5. Sorting an array: You can sort the elements of an array in ascending or descending order by using the sort() function from the algorithm library. Here is an example of how to sort the elements of an array in ascending order: 

```cpp
#include <algorithm>

int arr[5] = {3, 1, 4, 2, 5};

std::sort(arr, arr + 5); // Sort the elements of the array in ascending order
```
These are just a few examples of the operations that can be performed on arrays in C++. There are many other operations that can be performed on arrays, and the specific operations that are available depend on the programming language you are using.

> We are now going to see different kind of operations in Array. So let's get straight into the code. I am using C++ for these operations.
### Code
```cpp
// Array Operations Tutorial: [Display, Insert, Search, Update, Delete]
#include <iostream>
#define MAX 10
using namespace std;
int n;
void displayArray(int arr[], int n) {
  for (int i = 0; i < n; i++) {
    cout << arr[i] << " ";
  }
  cout << endl;
}
// Here size of array should be called by address
void insert(int arr[], int &n, int element, int index) {
  if (index >= MAX || n == MAX) {
    cout << "Error: array limit reached!!!" << endl;
    return;
  } else {
    cout << "Inserted: " << element << endl;
    if (index == n) {
      arr[index] = element;
      n++;
      return;
    }
    for (int i = n; i > index; i--) {
      arr[i] = arr[i - 1]; // Swapping values to get empty place at index
    }
    arr[index] = element;
    n++; // *Important: It's really important to increase the size
    return;
  }
}
void update(int index, int updatedValue, int arr[]) {
  if (index >= MAX) {
    cout << "Error: update index out of range!!!" << endl;
    return;
  }
  cout << "Updated value at index: " << index << endl;
  arr[index] = updatedValue;
  return;
}
void search(int element, int arr[], int n) {
  for (int i = 0; i < n; i++) {
    if (arr[i] == element) {
      cout << "Element found at index: " << i << endl;
      return;
    }
  }
  cout << "Element is not present in the array!!" << endl;
}
// Here also we should pass n as call by address as this value should persist
void remove(int arr[], int &n, int index) {
  if (index >= n) {
    cout << "Error: remove index out of range!!!" << endl;
    return;
  }
  for (int i = index; i < n - 1; i++) {
    arr[i] = arr[i + 1];
  }
  n--; // *Important: It's really important to decrease the size
  cout << "Deleted value at index: " << index << endl;
}
int main() {
  // This is the driver code for this tutorial you can change it as your own
  // preference like you can make it menu driven program if you want. I hope it
  // is now totatlly clear how different array operation works. 
  int arr[MAX];
  cout << "Enter the number of initial array elements: ";
  cin >> n;
  cout << "Now enter the array elements\n";
  for (int i = 0; i < n; i++) {
    cin >> arr[i];
  }
  insert(arr, n, 10, 2);
  displayArray(arr, n);
  update(2, 100, arr);
  displayArray(arr, n);
  search(12, arr, n);
  remove(arr, n, 7);
  remove(arr, n, 4);
  remove(arr, n, 1);
  displayArray(arr, n);
  return 0;
}
```
### Output
```
Enter the number of initial array elements: 5
Now enter the array elements
4 7 10 9 2
Inserted: 10
4 7 10 10 9 2 
Updated value at index: 2
4 7 100 10 9 2 
Element is not present in the array!!
Error: remove index out of range!!!
Deleted value at index: 4
Deleted value at index: 1
4 100 10 2
```
