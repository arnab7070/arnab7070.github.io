---
title: Binary Search Tree 
image: BST.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: All types of important operations in Binary Search Tree has been implemented. 
---
## Some Basic Concepts
A binary search tree (BST) is a data structure that is used to store data in a sorted and searchable manner. It consists of nodes organized in a tree-like structure, where each node has at most two children. The left child of a node contains a value that is less than the value of the parent node, and the right child contains a value that is greater than the value of the parent node. This means that the values of the nodes in the left subtree of a node are all less than the value of the node, and the values of the nodes in the right subtree are all greater than the value of the node.

Binary search trees have the following properties:

* The left subtree of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* The left and right subtree each must also be a binary search tree.
Binary search trees are often used for fast data insertion, deletion, and search operations, as the time complexity of these operations is O(log n) in the average case and O(n) in the worst case, where n is the number of nodes in the tree.

Some common operations that can be performed on a binary search tree include inserting a new node, deleting a node, searching for a particular value, and traversing the tree in different orders (such as in-order, pre-order, and post-order)
> We are now going to see different kind of operations in Binary Search Tree. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <iostream>
using namespace std;
class Node {
public:
  int data;
  Node *left;
  Node *right;

  // Constructor
  Node(int data) {
    this->data = data;
    this->left = NULL;
    this->right = NULL;
  }
};

Node *insert(Node* &root, int data) {
  if (root == NULL) {
    root = new Node(data);
    return root;
  }
  if (data > root->data) {
    root->right = insert(root->right, data);
  } else {
    root->left = insert(root->left, data);
  }
  return root;
}
// Inorder Traversal gives us sorted order list for BST
void inorder(Node *root) {
  if (root == NULL) {
    return;
  }
  inorder(root->left);
  cout << root->data << " ";
  inorder(root->right);
}
void preorder(Node *root) {
  if (root == NULL) {
    return;
  }
  cout << root->data << " ";
  inorder(root->left);
  inorder(root->right);
}
void postorder(Node *root) {
  if (root == NULL) {
    return;
  }
  postorder(root->left);
  postorder(root->right);
  cout << root->data << " ";
}
int height(Node *root) {
  if (root == NULL) {
    return 0;
  }
  int lHeight = height(root->left);
  int rHeight = height(root->right);

  return max(lHeight, rHeight) + 1;
}
bool search(Node *root, int key) {
  bool ans = false;
  if (root == NULL) {
    return ans;
  }
  // Data exist condition
  if (key == root->data) {
    cout << "Data Found!!" << endl;
    return true;
  }
  if (key > root->data) {
    search(root->right, key);
  } else {
    search(root->left, key);
  }
  return ans;
}

int smallest(Node *root) {
  // simple concept
  while (root->left != NULL) {
    root = root->left;
  }
  return root->data;
}
int largest(Node *root) {
  // simple concept
  while (root->right != NULL) {
    root = root->right;
  }
  return root->data;
}
int totalNodes(Node *root) {
  if (root == NULL) {
    return 0;
  }
  int lNodes = totalNodes(root->left);
  int rNodes = totalNodes(root->right);

  return lNodes + rNodes + 1;
}
// The nodes which are not leaf nodes -> Internal Nodes
int totalInternalNode(Node *root) {
  if (root == NULL) {
    return 0;
  }
  if (root->left == NULL && root->right == NULL) {
    return 0;
  }
  return (totalInternalNode(root->left) + totalInternalNode(root->right) + 1);
}
// The nodes which are leaf nodes -> External Nodes
int totalExternalNode(Node *root) {
  // Simple Solution
  // return (totalNodes(root)-totalInternalNode(root));

  // Complex Solution or Traditional Solution
  if (root == NULL) {
    return 0;
  }
  if (root->left == NULL && root->right == NULL) {
    return 1;
  }
  return (totalExternalNode(root->left) + totalExternalNode(root->right));
}
int sumOfNodes(Node *root) {
  if (root == NULL) {
    return 0;
  }
  return (sumOfNodes(root->right) + sumOfNodes(root->left) + root->data);
}

Node* deleteFromBST(Node* root, int data){
	//Base case
	if(root == NULL){
		return root;
	}
	if(root->data == data){
		// Main deletion operation will be handled here
		// Here we will handle 3 cases

		// Case 1: 0 Child
		if(root->right==NULL && root->left==NULL){
			// Perform delete to free the memory
			delete root;
			// Make that node points to NULL
			return NULL;
		}
		// Case 2: 1 Child
		// Here comes two sub-cases
		// Sub-Case 1: Right Child Exists
		if(root->right != NULL && root->left == NULL){
			// Store the right child 
			Node* temp = root->right;
			// Perform delete
			delete root;
			// Return the right child 
			return temp;
		}
		// Sub-Case 2: Left Child Exists
		if(root->right == NULL && root->left != NULL){
			// Store the left child 
			Node* temp = root->left;
			// Perform delete
			delete root;
			// Return the right child 
			return temp;
		}
		// Case 3: 2 Children
		if(root->left != NULL && root->right != NULL){
			// Step No. 1: We have to find the minimum value of right subtree
			// Or we can find out the maximum value of left subtree
			// any one of these will work fine. I will go for the first one.
	
			// Find the minimum value from right subtree
			int minValue = smallest(root->right);
			// Step No. 2: Copy that value to the present node
			root->data = minValue;
			//  Step No. 3: 
			// Now the data is successfully copied so we don't need that node
			// That's why we need to delete it from the right subtree because
			// we know that it is present on the right subtree
			root->right = deleteFromBST(root->right,minValue);
			// Step No.4: Now return the root for final operation
			return root;
		}
	}
	// If value is greater than root->data
	else if(data > root->data){
		//We are calling the function for the right sub-tree
		root->right = deleteFromBST(root->right, data);
		return root;
	}
	// If value is lesser than root->data
	else{
		//We are calling the function for the left sub-tree
		root->left = deleteFromBST(root->left, data);
		return root;
	}
}

int main() {
  /*

                               6
                             /   \
                            4	  9
                          /  \     \
                         1	  5	   11
  */

  Node *root = NULL;
  insert(root, 6);
  insert(root, 4);
  insert(root, 9);
  insert(root, 1);
  insert(root, 5);
  insert(root, 11);
  inorder(root);
  cout << endl;
  preorder(root);
  cout << endl;
  postorder(root);
  cout << endl;
  cout << "Height of the tree is: " << height(root) << endl;
  search(root, 4);
  if (!search(root, 10)) {
    cout << "Data doesn't exist!!" << endl;
  }
  cout << smallest(root) << endl;
  cout << largest(root) << endl;
  cout << totalNodes(root) << endl;
  cout << totalInternalNode(root) << endl;
  cout << totalExternalNode(root) << endl;
  cout << sumOfNodes(root) << endl;
  root = deleteFromBST(root, 4);
  inorder(root);
  cout<<endl;
  cout<<totalNodes(root)<<endl;
}
```
### Output
```
1 4 5 6 9 11 
6 1 4 5 9 11 
1 5 4 11 9 6 
Height of the tree is: 3
Data Found!!
Data doesn't exist!!
1
11
6
3
3
36
1 5 6 9 11 
5
```
