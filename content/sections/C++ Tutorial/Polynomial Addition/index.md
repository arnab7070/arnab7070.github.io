---
title: Polynomial Addition
image: Polynomial.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Here we need to add two polynomials using Linked List. So let's see how we can do it??
---
> Now we will do an important question for interview preparation. We need to add two polynomials using Linked List. So let's see how we can do it??

# Algorithm
---
#### Recursive Approach (Easy)
>1. If both the numbers are null then return.
>2. else if compare the power, if same then  add the coefficients and recursively call  
addPolynomials on the next elements of both the numbers.
>3. else if the power of first number is greater then print the current element of first number 
and recursively call addPolynomial on the next element of the first number and current element 
of the second number.
>4. else print the current element of the second number and recursively call addPolynomial on the 
current element of first number and next element of second number.
---
# C++ Implementation Code
---
```cpp
#include<iostream>
using namespace std;

/* 
Question
-------------------------------------------------------------------------------------------
let two polynomial be (4x^5 + 3x^4 + 5x^2 + 4x + 8) & (6x^5 + 7x^3 + 2x^2 + 8x + 10).
Now write a fuction to add these two polynomial equations.
*/

class node{
    public:
    int coeff;
    int power;
    node* next;

    //Constructor
    node(int coeff, int power){
        this->coeff = coeff;
        this->power = power;
        this->next = NULL;
    }
};
   
void addPolynomials(node *head1, node *head2){

    if(head1==NULL && head2==NULL){
        return;
    }
    else if(head1->power == head2->power){
        cout<<" "<<head1->coeff +  head2->coeff<<"x^"<<head1->power<<" ";
        addPolynomials(head1->next,head2->next);
    }
    else if(head1->power > head2->power){
        cout<<" "<<head1->coeff<<"x^"<<head1->power<<" ";
        addPolynomials(head1->next,head2);
    }
    else{
        cout<<" "<<head2->coeff<<"x^"<<head2->power<<" ";
        addPolynomials(head1,head2->next);
    }
}

int main()
{

    // (4x^5 + 3x^4 + 5x^2 + 4x + 8) 
    node* head1 = new node(4,5);
    head1->next = new node(3,4);
    head1->next->next = new node(5,2);
    head1->next->next->next = new node(4,1);
    head1->next->next->next->next = new node(8,0);
    // (6x^5 + 7x^3 + 2x^2 + 8x + 10)
    node* head2 = new node(6,5);
    head2->next = new  node(7,3);
    head2->next->next = new node(2,2);
    head2->next->next->next = new node(8,1);
    head2->next->next->next->next = new node(10,0);
    cout<<"Answer: ";
    addPolynomials(head1,head2);

    return 0;
}
```
---
# Output
---
```
Answer:  10x^5  3x^4  7x^3  7x^2  12x^1  18x^0
```
