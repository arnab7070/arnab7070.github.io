---
title: "Abstract Data Types"
image: module1.png
date: 2023-07-24T18:27:22+05:30
draft: false
description: Abstract Data Types (ADTs) are data structures hiding implementation details. They're defined by their state, operations, and invariants. Implementation involves specifying a concrete state, invariant, abstraction function, and operations.
---

# What is an abstract data type?

An abstract data type (ADT) is a mathematical model for data types. It specifies the operations that can be performed on the data, but it does not specify how the data is stored or implemented. This allows the ADT to be implemented in different ways, without affecting the way that it is used.

# Abstract Data Types and Their Specification

- An abstract data type (ADT) is a high-level description of a data structure or class that emphasizes its behavior and operations, rather than its specific implementation  .
- It defines a set of values and a set of operations on those values.
- It does not specify how data will be organized in memory and what algorithms will be used for implementing the operations.
- It is called "abstract" because it gives an implementation-independent view.
- The user of an ADT does not need to know how it is implemented, only what it can do.
- An ADT can be seen as a black box that hides the inner structure and design of the data type.

# How to Implement an ADT

- To implement an ADT, we need to choose a concrete data structure that can store the values and support the operations of the ADT.
- We also need to write the code for each operation, using the chosen data structure and algorithms.
- The implementation details are hidden from the user by using encapsulation and abstraction techniques.
- For example, we can implement a List ADT using a dynamic array or a linked list as the concrete data structure, and write the code for operations such as get, insert, remove, replace, size, isEmpty, isFull etc. 
- The user of the List ADT does not need to know whether it is implemented using an array or a linked list, only how to use the operations.

# Concrete state space
The concrete state space of an ADT is the set of all possible values that the data can take on. The concrete state space is implementation-dependent, meaning that it depends on how the ADT is implemented.

# Concrete invariant
The concrete invariant of an ADT is a property that must be true for all valid states of the data. The concrete invariant is also implementation-dependen.

# Concrete State Space, Concrete Invariant, Abstraction Function

- A `concrete state space` is the set of all possible states that the concrete data structure can have .
- A `concrete invariant` is a property that holds for all states in the concrete state space .
- An abstraction function is a mapping from the concrete state space to the abstract state space, which preserves the essential features of the ADT .
- For example, if we implement a Stack ADT using an array-based stack, then:
    - The concrete state space is the set of all possible arrays of a fixed size that can store elements of a given type.
    - The concrete invariant is that there is an integer variable `top` that indicates the index of the top element in the stack, and `0 <= top < size`, where `size` is the capacity of the array.
    - The abstraction function is a mapping from an array-based stack to a sequence of elements that represents the contents of the stack from top to bottom.

# Implementing Operations, Illustrated by the Text Example

- To implement an operation of an ADT, we need to write a function or method that takes some input parameters and returns some output values or modifies the state of the ADT .
- The function or method should follow the specification of the operation given by the ADT, and maintain the concrete invariant and abstraction function.
- For example, if we implement a Text ADT using a string as the concrete data structure, then:
    - The concrete state space is the set of all possible strings that can store characters.
    - The concrete invariant is that there is no limit on the length of the string.
    - The abstraction function is a mapping from a string to a sequence of characters that represents the contents of the text.
    - To implement an operation such as `insert(pos,c)`, which inserts a character `c` at position `pos` in the text, we can write a function like this (in pseudocode):

```java
ADT Text {
  operations:
    * get_text(): string
    * set_text(string text): void
    * is_empty(): bool

  axioms:
    * get_text() != "" if and only if is_empty() == false
}
```

I hope this helps you with your exam preparation. Good luck! 👍

- [Abstract Data Types - GeeksforGeeks](https://www.geeksforgeeks.org/abstract-data-types/)
- [Abstract Data Type in Data Structure - JavaTpoint](https://www.javatpoint.com/abstract-data-type-in-data-structure)
- [Abstract Data Types - University of Waterloo](https://ece.uwaterloo.ca/~dwharder/aads/Abstract_data_types/)
