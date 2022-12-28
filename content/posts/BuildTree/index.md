---
title: "BuildTree"
date: 2022-10-11T12:10:15+05:30
draft: false
image: BuildTree.png
description: Build a tree with Inorder & Preorder traversal array
tags: ["DSA","Tree"]
---
# Question
> Write a code to build a tree from the inorder and preorder traversal
---
# Concepts
In order to build a tree we can not only depend on the inorder. We must have one more traversal like postorder or preorder side by side. In this article we are going to see how we can implement a Build Tree function with a given preorder and inorder traversal. 

* Now from the preorder sequence we know that the leftmost element is the root of the tree. Now we will search that node in inorder sequence and find elements on the left side of root node and those to the right. 
* From inorder sequence we have to find out the index of the root and then the elements of it's left are the left subtree and the elements to the right is right subtree. So, we call the function recursively to build the tree.
# Code
```cpp
//build tree from inorder & preorder sequence
#include<iostream>
using namespace std;
struct Node{
    int data;
    struct Node* right;
    struct Node* left;

   Node(int val){
       data = val;
       right = NULL;
       left = NULL;
    } 
};

int search(int inorder[],int start, int end, int curr){
    for(int i = start; i<=end; i++){
        if(inorder[i]==curr){
            return i;
        }
    }
    return -1;
}
Node* buildTree(int preorder[], int inorder[], int start, int end){
    static int index  =  0;
    if(start>end){
        return NULL;
    }
    int curr = preorder[index];
    index++;
    Node* node = new Node(curr);
    if(start==end){
        return node;
    }
    int pos = search(inorder, start, end, curr);
    node->left = buildTree(preorder,inorder,start,pos-1);
    node->right = buildTree(preorder,inorder,pos+1,end);
    return node;
}
void inorderPrint(Node* root){
    if(root == NULL){
        return;
    }
    inorderPrint(root->left);
    cout<<root->data<<" ";
    inorderPrint(root->right);
}
int main(){

    int preorder[]={1,2,4,3,5};
    int inorder[]={4,2,1,5,3};

    Node* root = buildTree(preorder,inorder,0,4);
    inorderPrint(root);

return 0;
}
```

# Output
---
```cpp
4 2 1 5 3 
```