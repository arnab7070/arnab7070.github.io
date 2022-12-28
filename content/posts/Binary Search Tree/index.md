---
title: "Binary Search Tree"
date: 2022-09-29
tags: [DSA, C++, BST]
image: BST.png
description: C++ code to implement Binary Search Tree.
draft: false
---
# Implementation of Binary Search Tree
---
# Question
---
> Write a menu driven program in C or C++ to perform the following operations on Binary Search Tree.
> 1. insert a node.
> 2. inorder traversal.
> 3. preorder traversal.
> 4. postorder traversal.
> 5. search an given key.
> 6. Find the smallest element.
> 7. Find the largest element.
> 8. Delete an element.
> 9. Count the total number of nodes.
> 10. Count the total number of external nodes.
> 11.  Count the total number of internal nodes.
> 12. Determine the height of the tree.
---
# Code
---
```cpp
#include<iostream>

using namespace std;
class node{
    public:
    int data;
    node* right;
    node* left;

    //Constructor
    node(int data){
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};
class BST{
    public:
    node* insert(node* root, int item){
        if(root==NULL){
            return new node(item);
        }
        if(root->data > item){
            root->left = insert(root->left, item);
        }
        else{
            root->right = insert(root->right, item);
        }
        return root;
    }

    void preorder(node *root){
        if(root==NULL){
            return;
        }
        cout<<root->data<<" ";
        preorder(root->left);
        preorder(root->right);
    }

    void postorder(node *root){
        if(root==NULL){
            return;
        }
        postorder(root->left);
        postorder(root->right);
        cout<<root->data<<" ";
    }

    void inorder(node *root){
        if(root==NULL){
            return;
        }
        inorder(root->left);
        cout<<root->data<<" ";
        inorder(root->right);
    }

    int treeHeight(node* root){
        if(root==NULL){
            return 0;
        }
        int h1 = treeHeight(root->right);
        int h2 = treeHeight(root->left);

        return max(h1,h2)+1;
    }


    int countNodes(node* root){
        //base case
        if(root==NULL){
            return 0;
        }
        return countNodes(root->right)+countNodes(root->left)+1;
    }

    int maxNodeVal(node* root){
        if(root==NULL){
            return 0;
        }
        if(root->right==NULL){
            return root->data;
        }
        maxNodeVal(root->right);
    }

    int minNodeVal(node* root){
        if(root==NULL){
            return 0;
        }
        if(root->left==NULL){
            return root->data;
        }
        minNodeVal(root->left);
    }
	
	bool search(node* root, int key){
		while(root!=NULL){
			if(root->data == key){
				return true;
			}
			if(key>root->data){
				root = root->right;
			}
			else{
				root = root->left;
			}
		}
		return false;
	}
	
	int totalInternalNode(node* root){
		if(root==NULL){
			return 0;
		}
		if(root->right==NULL && root->left==NULL){
			return 0;
		}
		return (totalInternalNode(root->left)+totalInternalNode(root->right)+1);
	}
	
	int totalExternalNode(node* root){
		if(root==NULL){
			return 0;
		}
		if(root->right==NULL && root->left==NULL){
			return 1;
		}
		return (totalExternalNode(root->left)+totalExternalNode(root->right));
	}
};
int main()
{
    BST bst;
    node* root = NULL;
    system("clear");
    while(1){
    	cout<<"1.Insert\n2.Inorder\n3.Preorder\n4.Postorder\n5.Search\n6.Find Smallest\n7.Find Largest\n8.Total Nodes\n9.Total External Nodes\n10.Total Internal Nodes\n11.Height of Tree\n0.Exit"<<endl;
    	cout<<"--------------------------------------------------------------------------------"<<endl;
    	cout<<"Enter any option: ";
    	int key;
    	cin>>key;
    	switch(key){
    		case 1:
    			int element;
    			cout<<"Enter the value to insert: "<<endl;
    			cin>>element;
    			root = bst.insert(root,element);
    			break;
    		case 2:
    			bst.inorder(root);
    			cout<<endl;
    			break;
    		case 3:
    			bst.preorder(root);
    			cout<<endl;
    			break;
    		case 4:
    			bst.postorder(root);
    			cout<<endl;
    			break;
    		case 5:
    			cout<<"Enter an element to search: "<<endl;
    			int n;
    			cin>>n;
    			if(bst.search(root,n)){
    				cout<<"Yes element is present"<<endl;
    			}
    			else{
    				cout<<"Element is not present"<<endl;
    			}
    			break;
    		case 6: 
    			cout<<"The smallest number is: "<<bst.minNodeVal(root)<<endl;
    			break;
    		case 7:
    			cout<<"The largest number is: "<<bst.maxNodeVal(root)<<endl;
    			break;
    		case 8:
    			cout<<"Total nodes in the tree: "<<bst.countNodes(root)<<endl;
    			break;
    		case 9:
    			cout<<"Total external node in the tree: "<<bst.totalExternalNode(root)<<endl;
    			break;
    		case 10:
    			cout<<"Total internal node in the tree: "<<bst.totalInternalNode(root)<<endl;
    			break;
    		case 11:
    			cout<<"Total height of the tree: "<<bst.treeHeight(root)<<endl;\
    			break;
    		default:
				cout<<"Thanks for using BST Data Structure"<<endl;
				return 0;
    	}
    }
    
    return 0;
}
```
# Output
---
```cpp
1. Insert
2. Inorder
3. Preorder
4. Postorder
5. Search
6. Find Smallest
7. Find Largest
8. Total Nodes
9. Total External Nodes
10. Total Internal Nodes
11. Height of Tree
0. Exit
--------------------------------------------------------------------------------
Enter any option: 1
Enter the value to insert: 10
Enter any option: 1
Enter the value to insert: 5
Enter any option: 1
Enter the value to insert: 15
Enter any option: 1
Enter the value to insert: 12
Enter any option: 1
Enter the value to insert: 7
Enter any option: 2
5 7 10 12 15
Enter any option: 3
10 5 7 15 12
Enter any option: 4
7 5 12 15 10
Enter any option: 5
Enter an element to search:
12
Yes element is present
Enter any option: 5
Enter an element to search:
20
Element is not present
Enter any option: 6
The smallest number is: 5
Enter any option: 7
The largest number is: 15
Enter any option: 8
Total nodes in the tree: 5
Enter any option: 9
Total external node in the tree: 2
Enter any option: 10
Total internal node in the tree: 3
Enter any option: 11
Total height of the tree: 3
```