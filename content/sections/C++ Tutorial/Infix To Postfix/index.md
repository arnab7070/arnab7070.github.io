---
title: 8. Infix To Postfix
image: ITP.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: Here we will see how we can easily code our Infix to Postfix conversion. 
---
## Some Basic Concepts
Infix notation is a common way of writing arithmetic expressions in which the operators are written between the operands, such as "3 + 4". On the other hand, postfix notation (also known as reverse Polish notation) is a notation in which the operators are written after the operands, such as "3 4 +".

Converting an infix expression to a postfix expression can be done using a stack. The basic idea is to scan the infix expression from left to right, and use a stack to keep track of the operators. The algorithm works as follows:

1. Initialize an empty stack.
2. Scan the infix expression from left to right.
3. If the current character is an operand, add it to the output string (which will eventually contain the postfix expression).
4. If the current character is an operator, follow these steps:
   1. While the stack is not empty and the top element of the stack has equal or higher precedence than the current operator, pop the top element from the stack and add it to the output string.
   2. Push the current operator onto the stack.
5. If the current character is a left parenthesis, push it onto the stack.
6. If the current character is a right parenthesis, follow these steps:
   1. While the top element of the stack is not a left parenthesis, pop the top element from the stack and add it to the output string.
   2. Pop the left parenthesis from the stack (but do not add it to the output string).
7. Repeat steps 2-7 until the end of the infix expression is reached.
8. While the stack is not empty, pop the top element from the stack and add it to the output string.

> We are now going to see the code of Infix to Postfix conversion. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <bits/stdc++.h>
using namespace std;

int precedence(char ch){
    switch(ch){
		//If the operator is Plus or Minus
        case '-':
        case '+':
            return 1;
		//If the operator is Multiplier or Divider
        case '*':
        case '/':
            return 2;
		//If the operator is a Power
		case '^':
			return 3;
        default:
            return -1;
    }
}
bool isOperand(char ch){
	// If the character is an operand return true otherwise return false
    return (ch>='a' && ch<='z') || (ch>='A' && ch <='Z' || (ch>='0' && ch<='9'));
}
// Function to convert infix to postfix expression
string infixToPostfix(string infix){
	// n = length of the infix expression
    int n=infix.length();
	//we are using inbuilt stack library of char datatype
    stack<char> st;
	//this is the main string where we store our answer
    string postfix;
	//now iterate all over the infix expression 
    for(int i=0;i<n;i++){
        if(isOperand(infix[i])){
            //step 2 -> if it is an operand directly push it to the postfix string
            postfix.push_back(infix[i]);
        }
        else if(infix[i] == '('){
            //step 3 -> if it is opening bracket just push it to the postfix string
            st.push('(');
        }
        else if(infix[i] == ')'){
            //step 4 -> if we encounter an closing bracket then just pop all the elements
			// & push it to the main answer string until we reach to the opening bracket
            while( st.top() != '(' ){
                postfix.push_back(st.top());
                st.pop();
            }
			// Now throw '(' out of the stack
            st.pop();
            
        }
        else{
            // step 5 -> if the precedence of the incoming character is lesser than the stack
			// top character then first pop the stack top character and add it to the postfix
			// string. Do this until incoming operator precedence is greater than the stack top
			// operator. (Fun remembrance 😉: Toppers always take the top position in the class)
            while(!st.empty() && st.top() != '(' && precedence(st.top()) >= precedence(infix[i])){
                postfix.push_back(st.top());
                st.pop();
            }
			// pushing the incoming operator finally to the stack
            st.push(infix[i]);
        }
    }
    // Now finally add all rest elements into the postfix string until stack gets empty
    while(!st.empty()){
        postfix.push_back(st.top());
        st.pop();
    }
    return postfix;
}

int main() {
	// main driver code for this operation
    string infix;
	cout<<"Enter the infix expression: ";
	cin>>infix;
    string postfix=infixToPostfix(infix);
    cout<<"Infix expression : "<<infix<<endl; 
    cout<<"Postfix expression : "<<postfix<<endl;
    return 0;
}
```
### Output
```
Enter the infix expression: 2+3*(4/5)-6
Infix expression : 2+3*(4/5)-6
Postfix expression : 2345/*+6-
```
