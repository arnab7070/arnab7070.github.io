---
title: "Command Line Argument in C++"
description: "Exploring command line arguments in C++ programming."
date: 2024-02-18T09:23:32+05:30
draft: false
image: keyboard.jpg
tags: ["C++", "DSA"]
---

When working with C++ programs, it's often necessary to interact with the command line. Command line arguments allow us to pass inputs to our program when executing it from the terminal. In this blog post, we'll explore how to handle command line arguments in C++ using a simple program.

Let's start by examining the following C++ code:

```cpp
#include <iostream>
using namespace std;

int main(int argc, char *argv[])
{
    // argc -> Argument Count, argv -> Argument Vector
    // By default, the value of argc is 1
    if (argc < 2)
    {
        cout << "Enter command line inputs" << endl;
        return 1;
    }
    for (int i = 1; i < argc; i++)
    {
        // argv[0]: C:\Users\sf745\Desktop\Github\Codes\C++ Programs\DSA Concepts\commandLine.exe
        cout << "argv[" << i << "]: " << argv[i] << endl;
    }
    return 0;
}
```

This code snippet defines a simple C++ program that demonstrates how to handle command line arguments. Here's a breakdown of what's happening:

- The `main` function takes two parameters: `argc`, which stands for "argument count", and `argv`, which stands for "argument vector". `argc` represents the number of arguments passed to the program, and `argv` is an array of strings containing those arguments.
- Inside `main`, we first check if the number of arguments (`argc`) is less than 2. If so, we print a message instructing the user to enter command line inputs, and then we return 1 to indicate an error.
- If there are command line arguments, we use a `for` loop to iterate over each argument. We start from index 1 (`i = 1`) because `argv[0]` typically contains the name of the program itself.
- Within the loop, we print each argument along with its index using `cout`.

To compile and execute this program, you can follow these steps:

1. Save the code to a file (e.g., `commandLine.cpp`).
2. Compile the code using a C++ compiler. For example, you can use `g++`:
   ```
   g++ commandLine.cpp -o commandLine
   ```
3. Execute the compiled program with command line arguments. For example:
   ```
   ./commandLine arg1 arg2 arg3
   ```

Replace `arg1`, `arg2`, and `arg3` with any desired command line inputs. The program will then display each argument along with its index.

Understanding how to handle command line arguments is essential for building robust and flexible C++ applications. Whether you're developing command-line utilities or larger software projects, mastering this concept will empower you to create more versatile programs.

That wraps up our exploration of command line arguments in C++! Stay tuned for more insights and tutorials on C++ programming and other topics.