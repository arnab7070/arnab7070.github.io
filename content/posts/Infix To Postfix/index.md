---
title: Infix to Postfix
date: 2022-10-10
description: C++ implementation to convert an infix mathematical expression to postfix.
tags: ["DSA","Postfix Conversion"]
image: InfixToPostfix.png
draft: false
---
# Question
> Convert infix expression to postfix expression using C++
# Some Important Concepts
* Infix notation is the notation in which operators come between the required operands.
* Postfix notation is the type of notation in which operator comes after the operand.
* Infix expression can be converted to postfix expression using stack.
---
# Code
```cpp
#include<iostream>
#include<math.h>
#include<stack>
using namespace std;
int precedence(char c){
    if (c=='^')
    {
        return 3;
    }
    else if (c=='*'||c=='/')
    {
        return 2;
    }
    else if(c=='+'||c=='-'){
        return 1;
    }
    else{
        return -1;
    }
}
string infixToPostfix(string s){
    stack<char> st;
    string result;
    for(int i = 0; i < s.length(); i++){
        if(s[i]>='a'&&s[i]<='z'||s[i]>='A'&&s[i]<='Z'){
            result+=s[i];    
        }
        else if(s[i]=='('){
            st.push(s[i]);
        }
        else if(s[i]==')'){
            while(!st.empty()&&st.top()!='('){
                result+=st.top();
                st.pop();
            }
            if (!st.empty())
            {
                st.pop();
            } 
        }
        else{
            while (!st.empty()&&precedence(st.top())>precedence(s[i]))
            {
                result+=st.top();
                st.pop();
            } 
            st.push(s[i]);
        }
    }
    while (!st.empty())
    {
        result+=st.top();
        st.pop();
    }
    
    return result;
}
int main(){

   cout<<infixToPostfix("(a-b/c)*(a/k-l)")<<endl;

return 0;
}
```
# Output
```cpp
abc/-ak/l-*
```