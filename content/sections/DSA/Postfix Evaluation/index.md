---
title: 9. Postfix Evaluation
image: evaluation.gif
date: 2022-12-27
tags: ["C++","LAB EXAM","ONESHOT"]
draft: false
description: C++ implementation of Postfix evaluation. It's really easy!!!
---
## Some Basic Concepts
Postfix notation (also known as reverse Polish notation) is a way of writing arithmetic expressions in which the operands are written before the operators. For example, the expression "3 4 +" is written in postfix notation and means "3 + 4".

Evaluating a postfix expression involves scanning the expression from left to right and using a stack to keep track of the operands. The algorithm works as follows:

1. Initialize an empty stack.
2. Scan the postfix expression from left to right.
3. If the current character is an operand, push it onto the stack.
4. If the current character is an operator, follow these steps:
    1. Pop the top two elements from the stack.
    2. Apply the operator to the two operands.
    3. Push the result onto the stack.
5. Repeat steps 2-4 until the end of the expression is reached.
6. The result is the value at the top of the stack.

* It is important to note that the above algorithm assumes that the postfix expression is well-formed and does not contain any syntax errors. It is also important to handle the case where the stack is empty or has fewer than two elements, as this can lead to runtime errors.
> We are now going to see the code of Postfix Evaluation. It's an important question for stack based operations. So let's get straight into the code. I am using C++ for these operations.

### Code
```cpp
#include <cmath>
#include <iostream>
#include <stack>
using namespace std;

// function to calculate with respect to current incoming operator
int simpleCalculator(int a, int b, int op) {
  // switch the operator
  switch (op) {
  case '+':
    return a + b;
  case '-':
    return a - b;
  case '*':
    return a * b;
  case '/':
    return a / b;
  case '^':
    return pow(a, b);
  }
}

// function to evaluate the postfix expression
int postfixEvaluator(string postfix) {
  // create a stack of int data-type from C++ library
  stack<int> st;
  int answer = 0;
  // Now iterate over all of the characters of the string
  for (int i = 0; i < postfix.length(); i++) {
    // if a charcter is in between 0-9 then add it to the stack
    if (postfix[i] >= '0' && postfix[i] <= '9') {
      st.push(postfix[i] - '0');
    }
    // if we encounter some operator then we should pop two stack top elements
    // and evaluate them with the current operator
    else {
      int op2 = st.top();
      st.pop();
      int op1 = st.top();
      st.pop();
      // we directly now push the current evaluated value to the stack
      st.push(simpleCalculator(op1, op2, postfix[i]));
    }
  }
  // finally we get our final answer as stack top value
  return st.top();
}

int main() {
  string postfix_expression;
  cout << "Enter the postfix expression: ";
  cin >> postfix_expression;
  cout << "Evaluated value for this postfix expression: "
       << postfixEvaluator(postfix_expression) << endl;
}
```
### Output
```
Enter the postfix expression: 23+5*
Evaluated value for this postfix expression: 25
```
