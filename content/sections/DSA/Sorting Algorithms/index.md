---
title: Sorting Algorithms One Shot
image: Sorting.gif
date: 2023-01-26
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: We can now understand all of the sorting algorithms in one shot.
---
## Bubble Sort
---------------
#### Small Concept
```
Bubble Sort is a simple and basic sorting algorithm that repeatedly steps through the list to be sorted, compares each pair of adjacent items and swaps them if they are in the wrong order. This process is repeated until no swaps are needed, which indicates that the list is sorted.
```
#### Code
```cpp
void bubbleSort(int arr[], int n){
	int totalComparision = 0;
	for(int i = 0; i < n-1; i++){
		for(int j = 0; j < n-i-1; j++){
			totalComparision++;
			if(arr[j] > arr[j+1]){
				swap(arr[j],arr[j+1]);
			}
		}
	}
	cout<<"The sorted array will look like: ";
	print(arr,n);
	cout<<"Total number of comparisions required: "<<totalComparision<<endl;
}
```
## Insertion Sort
---------------
#### Small Concept
```
Insertion Sort is a simple sorting algorithm that builds the final sorted list one item at a time. It takes each element from the list and compares it to the elements already in the sorted portion of the list, and then places it in the correct position.
```
#### Code
```cpp
void insertionSort(int arr[], int n){
	int totalComparision = 0;
	for(int i = 1; i < n; i++){
		int current_element = arr[i];
		int j = i-1;
		while(arr[j] > current_element && j >= 0){
			totalComparision++;
			arr[j+1] = arr[j];
			j--;
		}
		arr[j+1] = current_element;
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
	cout<<"Total number of comparisions required: "<<totalComparision<<endl;
	
}
```
## Selection Sort
---------------
#### Small Concept
```
Selection Sort is another simple sorting algorithm that selects the smallest element from the unsorted portion of the list and places it at the beginning of the sorted portion of the list. This process is repeated until the entire list is sorted.
```
#### Code
```cpp
void selectionSort(int arr[], int n){
	int totalComparision = 0;
	for(int i = 0; i < n-1; i++){
		int minIndex = i;
		for(int j = i+1; j < n; j++){
			totalComparision++;
			if(arr[minIndex] > arr[j]){
				minIndex = j;
			}
		}
		swap(arr[i],arr[minIndex]);
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
	cout<<"Total number of comparisions required: "<<totalComparision<<endl;
}
```
## Merge Sort
---------------
#### Small Concept
```
Merge Sort is a divide-and-conquer algorithm that divides the input list into two sublists, recursively sorts the sublists and then merges the sorted sublists to produce the final sorted list.
```
#### Code
```cpp
void merge(int arr[], int start, int end){
	int mid = (start+end)/2;
	int len1 = mid-start+1;
	int len2 = end-mid;
	int first[len1];
	int second[len2];

	//Now copy the elements
	int mainArrayIndex = start;
	for(int i = 0; i < len1; i++){
		first[i] = arr[mainArrayIndex++];
	}
	for(int i = 0; i < len2; i++){
		second[i] = arr[mainArrayIndex++];
	}
	//Merge 2 sorted array
	int index1 = 0, index2 = 0;
	mainArrayIndex = start;

	while(index1 < len1 && index2 < len2){
		if(first[index1] < second[index2]){
			arr[mainArrayIndex++] = first[index1++];
		}
		else{
			arr[mainArrayIndex++] = second[index2++];
		}
	}
	while(index1 < len1){
		arr[mainArrayIndex++] = first[index1++];
	}
	while(index2 < len2){
		arr[mainArrayIndex++] = second[index2++];
	}
	
}

void mergeSort(int arr[], int start, int end){
	if(start >= end){
		return;
	}
	int mid = (start+end)/2;
	mergeSort(arr, start, mid);
	mergeSort(arr, mid+1, end);
	merge(arr, start, end);
}
```
## Heap Sort
---------------
#### Small Concept
```
Heap Sort is a comparison-based sorting algorithm that builds a binary heap from the input list and then repeatedly extracts the maximum element from the heap and places it at the end of the sorted list.
```
#### Code
```cpp
void heapify(int arr[], int n, int i){
	int largest = i;
	int left = 2*i + 1;
	int right = 2*i + 2;

	if(left < n && arr[left] > arr[largest]){
		largest = left;
	}
	if(right < n && arr[right] > arr[largest]){
		largest = right;
	}
	if(i != largest){
		swap(arr[i],arr[largest]);
		heapify(arr,n,largest);
	}
}
	
void heapSort(int arr[], int n){
	for(int i = n/2 - 1; i >= 0; i--){
		heapify(arr, n, i);
	}
	for(int i = n-1; i >= 0; i--){
		swap(arr[i],arr[0]);
		heapify(arr, i, 0);
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
}
```
## Count Sort
---------------
#### Small Concept
```
Count Sort is a sorting algorithm that uses the counts of each element to place them in their correct position in the sorted list. It is efficient for small integers and positive integers.
```
#### Code
```cpp
void countSort(int arr[], int n){
	int max_element = INT_MIN;
	for(int i = 0; i < n; i++){
		if(arr[i] > max_element){
			max_element = arr[i];
		}
	}
	int helper[max_element + 1];
	for(int i = 0; i < max_element+1; i++){
		helper[i] = 0;
	}
	for(int i = 0; i < n; i++){
		helper[arr[i]]++;
	}
	int index = 0;
	for(int i = 0; i < max_element+1; i++){
		while(helper[i] > 0){
			arr[index++] = i;
			helper[i]--;
		}
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
}
```
## Quick Sort 
---------------
#### Small Concept
```
Quick Sort is a divide-and-conquer algorithm that selects a "pivot" element from the list and partition the other elements into two sublists, according to whether they are less than or greater than the pivot. The sublists are then recursively sorted.
```
#### Code
```cpp
int partition(int arr[], int low, int high){
	int pivot = arr[high];
	int i = low-1;
	for(int j = low; j < high; j++){
		if(arr[j] < pivot){
			i++;
			swap(arr[i], arr[j]);
		}
	}
	i++;
	swap(arr[high], arr[i]);
	return i;
}

void quickSort(int arr[], int low, int high){
	if(low < high){
		int pivotIndex = partition(arr, low, high);
		quickSort(arr, low, pivotIndex-1);
		quickSort(arr, pivotIndex+1, high);
	}
}
```
All of these sorting algorithms have their own advantages and disadvantages, and the choice of algorithm depends on the specific use case and the characteristics of the input data.

## Full Code Implementation
```cpp
#include <iostream>
#include <climits>
using namespace std;
void print(int arr[], int n){
	for(int i = 0; i < n; i++){
		cout<<arr[i]<<" ";
	}
	cout<<endl;
}
void bubbleSort(int arr[], int n){
	int totalComparision = 0;
	for(int i = 0; i < n-1; i++){
		for(int j = 0; j < n-i-1; j++){
			totalComparision++;
			if(arr[j] > arr[j+1]){
				swap(arr[j],arr[j+1]);
			}
		}
	}
	cout<<"The sorted array will look like: ";
	print(arr,n);
	cout<<"Total number of comparisions required: "<<totalComparision<<endl;
}

void selectionSort(int arr[], int n){
	int totalComparision = 0;
	for(int i = 0; i < n-1; i++){
		int minIndex = i;
		for(int j = i+1; j < n; j++){
			totalComparision++;
			if(arr[minIndex] > arr[j]){
				minIndex = j;
			}
		}
		swap(arr[i],arr[minIndex]);
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
	cout<<"Total number of comparisions required: "<<totalComparision<<endl;
}

void insertionSort(int arr[], int n){
	int totalComparision = 0;
	for(int i = 1; i < n; i++){
		int current_element = arr[i];
		int j = i-1;
		while(arr[j] > current_element && j >= 0){
			totalComparision++;
			arr[j+1] = arr[j];
			j--;
		}
		arr[j+1] = current_element;
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
	cout<<"Total number of comparisions required: "<<totalComparision<<endl;
	
}

void countSort(int arr[], int n){
	int max_element = INT_MIN;
	for(int i = 0; i < n; i++){
		if(arr[i] > max_element){
			max_element = arr[i];
		}
	}
	int helper[max_element + 1];
	for(int i = 0; i < max_element+1; i++){
		helper[i] = 0;
	}
	for(int i = 0; i < n; i++){
		helper[arr[i]]++;
	}
	int index = 0;
	for(int i = 0; i < max_element+1; i++){
		while(helper[i] > 0){
			arr[index++] = i;
			helper[i]--;
		}
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
}


void heapify(int arr[], int n, int i){
	int largest = i;
	int left = 2*i + 1;
	int right = 2*i + 2;

	if(left < n && arr[left] > arr[largest]){
		largest = left;
	}
	if(right < n && arr[right] > arr[largest]){
		largest = right;
	}
	if(i != largest){
		swap(arr[i],arr[largest]);
		heapify(arr,n,largest);
	}
}
	
void heapSort(int arr[], int n){
	for(int i = n/2 - 1; i >= 0; i--){
		heapify(arr, n, i);
	}
	for(int i = n-1; i >= 0; i--){
		swap(arr[i],arr[0]);
		heapify(arr, i, 0);
	}
	cout<<"The sorted array will look like: ";
	print(arr, n);
}

int partition(int arr[], int low, int high){
	int pivot = arr[high];
	int i = low-1;
	for(int j = low; j < high; j++){
		if(arr[j] < pivot){
			i++;
			swap(arr[i], arr[j]);
		}
	}
	i++;
	swap(arr[high], arr[i]);
	return i;
}

void quickSort(int arr[], int low, int high){
	if(low < high){
		int pivotIndex = partition(arr, low, high);
		quickSort(arr, low, pivotIndex-1);
		quickSort(arr, pivotIndex+1, high);
	}
}

void merge(int arr[], int start, int end){
	int mid = (start+end)/2;
	int len1 = mid-start+1;
	int len2 = end-mid;
	int first[len1];
	int second[len2];

	//Now copy the elements
	int mainArrayIndex = start;
	for(int i = 0; i < len1; i++){
		first[i] = arr[mainArrayIndex++];
	}
	for(int i = 0; i < len2; i++){
		second[i] = arr[mainArrayIndex++];
	}
	//Merge 2 sorted array
	int index1 = 0, index2 = 0;
	mainArrayIndex = start;

	while(index1 < len1 && index2 < len2){
		if(first[index1] < second[index2]){
			arr[mainArrayIndex++] = first[index1++];
		}
		else{
			arr[mainArrayIndex++] = second[index2++];
		}
	}
	while(index1 < len1){
		arr[mainArrayIndex++] = first[index1++];
	}
	while(index2 < len2){
		arr[mainArrayIndex++] = second[index2++];
	}
	
}

void mergeSort(int arr[], int start, int end){
	if(start >= end){
		return;
	}
	int mid = (start+end)/2;
	mergeSort(arr, start, mid);
	mergeSort(arr, mid+1, end);
	merge(arr, start, end);
}

int main() {

	int n;
	cout<<"Enter the number of elements you want to insert in array: ";
	cin>>n;
	int arr[n];
	cout<<"Now enter the elements: ";
	for(int i = 0; i < n; i++){
		cin>>arr[i];
	}
	bubbleSort(arr, n);
	// selectionSort(arr, n);
	// insertionSort(arr, n);
	// countSort(arr, n);
	// heapSort(arr, n);
	// quickSort(arr, 0, n-1);
	// mergeSort(arr, 0, n-1);
	// cout<<"The sorted array will look like after: ";
	// print(arr, n);
	return 0;
	
}
```