---
title: "MVC & Memory Management"
date: 2023-07-28T06:38:06+05:30
draft: false
image: module4.png
description: This tutorial teaches you how to implement object-oriented programming in Java. You will learn about the model-view-controller pattern, commands as methods and as objects, and other OOP concepts.
---

# Model-view-controller pattern

- The model-view-controller (MVC) pattern is a design pattern that separates an application into three components: the model, the view, and the controller.
- The model represents the data and business logic of the application. It is responsible for managing the state and notifying the view of any changes.
- The view represents the presentation layer of the application. It is responsible for displaying the data from the model and receiving user input.
- The controller acts as an intermediary between the model and the view. It is responsible for handling user requests, updating the model, and selecting the appropriate view.
- The MVC pattern allows for a clear separation of concerns, modularity, reusability, and testability of the application components.

# Model

##### Role

- Data and business logic

##### Example

- Student class

# View

##### Role

- Presentation layer

##### Example

- StudentView class

# Controller

##### Role

- Intermediary between model and view

##### Example

- StudentController class

## Example of MVC pattern in Java

- To illustrate how to implement the MVC pattern in Java, let's create a simple example of a student management system.
- We will create a Student class that represents the model, a StudentView class that represents the view, and a StudentController class that represents the controller.
- The Student class will have two instance variables: name and rollNo. It will also have getters and setters for these variables.
- The StudentView class will have one instance method: printStudentDetails. This method will take a student name and roll number as parameters and print them to the console.
- The StudentController class will have two instance variables: model and view. It will also have a constructor that takes a Student object and a StudentView object as parameters and assigns them to the instance variables. It will also have methods to set and get the student name and roll number, and to update the view.

```java
// Model class
public class Student {
    private String name;
    private String rollNo;

    // getters and setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getRollNo() {
        return rollNo;
    }

    public void setRollNo(String rollNo) {
        this.rollNo = rollNo;
    }
}

// View class
public class StudentView {
    public void printStudentDetails(String studentName, String studentRollNo) {
        System.out.println("Student: ");
        System.out.println("Name: " + studentName);
        System.out.println("Roll No: " + studentRollNo);
    }
}

// Controller class
public class StudentController {
    private Student model;
    private StudentView view;

    // constructor
    public StudentController(Student model, StudentView view) {
        this.model = model;
        this.view = view;
    }

    // methods to set and get student name and roll number
    public void setStudentName(String name) {
        model.setName(name);
    }

    public String getStudentName() {
        return model.getName();
    }

    public void setStudentRollNo(String rollNo) {
        model.setRollNo(rollNo);
    }

    public String getStudentRollNo() {
        return model.getRollNo();
    }

    // method to update the view
    public void updateView() {
        view.printStudentDetails(model.getName(), model.getRollNo());
    }
}
```

- To test our MVC implementation, we will create a Main class that creates a Student object, a StudentView object, and a StudentController object. We will then use the controller to set and get the student data and update the view.

```java
// Main class
public class Main {
    public static void main(String[] args) {
        // create a student object
        Student student = new Student();
        student.setName("Alice");
        student.setRollNo("101");

        // create a student view object
        StudentView studentView = new StudentView();

        // create a student controller object
        StudentController studentController = new StudentController(student, studentView);

        // use the controller to update the view
        studentController.updateView();

        // use the controller to modify the student data
        studentController.setStudentName("Bob");

        // use the controller to update the view again
        studentController.updateView();
    }
}
```

- The output of running the Main class will be:

```
Student:
Name: Alice
Roll No: 101
Student:
Name: Bob
Roll No: 101
```

# Commands as methods and as objects

- A command is an action that can be performed by an object. In Java, a command can be represented as a method or as an object.
- A command as a method is a simple way of defining and executing a command. A method is a block of code that performs a specific task and can be invoked by other objects. A method can have parameters and a return value.
- A command as an object is a more advanced way of defining and executing a command. An object is an instance of a class that has fields and methods. A command object is an object that implements a specific interface or abstract class that defines the command's API. A command object can have fields to store the information required for executing the command, such as the receiver object, the method to call, and the method arguments. A command object can also have a method to execute the command, usually called execute or run.

## Example of commands as methods & as objects in Java

**1. Commands as Methods**

In Java, a method is a command that tells the computer to perform a certain action. It is a collection of statements that perform some specific task and return the result to the caller. A method can perform some specific task without returning anything. 

Here is an example of a command as a method in Java:

```java
public class Main {
    // Method named "printHelloWorld"
    public static void printHelloWorld() {
        System.out.println("Hello, World!");
    }

    public static void main(String[] args) {
        // Call the method named "printHelloWorld"
        printHelloWorld();
    }
}
```
In the above code, `printHelloWorld` is a method that commands Java to print "Hello, World!" to the console.

**2. Commands as Objects**

In some cases, you might want to encapsulate commands as objects. This is often used in design patterns like the Command Pattern, where an object is used to encapsulate all information needed to perform an action or trigger an event at a later time. 

Here's a simple example of a command as an object in Java:

```java
public interface Command {
    void execute();
}

public class HelloWorldCommand implements Command {
    public void execute() {
        System.out.println("Hello, World!");
    }
}

public class Main {
    public static void main(String[] args) {
        Command cmd = new HelloWorldCommand();

        // execute command
        cmd.execute();
    }
}
```

In this code, `HelloWorldCommand` is a class implementing the `Command` interface and defining the `execute` method, which prints "Hello, World!". In the `main` method, we create an instance of `HelloWorldCommand`, treat it as a `Command`, and call `execute`.

In this way, the command to print "Hello, World!" is encapsulated within the `HelloWorldCommand` object. This is an example of a command as an object in Java. It's a higher-level abstraction than a command as a method, and it's a way of using objects to represent real-world actions or events.

## Memory management in JAVA
Memory management in Java is primarily managed by the Java Virtual Machine (JVM) and one of its component called the Garbage Collector. It is part of the internal workings of the JVM and is abstracted away from the programmer for the most part, making memory management in Java a largely automatic process.

In Java, the memory is divided into two parts:

1. **Stack Memory**: Stack memory is used for the execution of a thread. It contains method-specific values that are short-lived. Stack memory is always referenced in LIFO (Last-In-First-Out) order.

2. **Heap Memory**: This is the runtime data area from which the memory for all class instances and arrays is allocated. The heap is created on the JVM start-up and shared among all Java Virtual Machine threads.

Here's an overview of how memory management works in Java.

**1. Object creation**

When you create an object in Java (using the `new` keyword), memory is allocated on the heap to hold the object's instance variables.

```java
Person person = new Person("John Doe", 30); // Allocates memory for a Person object on the heap
```

**2. Object use**

As long as an object is being referenced, it remains in memory. The object can be used by accessing its methods and fields through the reference.

```java
System.out.println(person.getName()); // Uses the person object
```

**3. Garbage collection**

When an object is no longer referenced anywhere, it becomes eligible for garbage collection. The Java Garbage Collector is a program running in the background that looks for unreferenced objects and frees the memory they are using.

```java
person = null; // Makes the person object eligible for garbage collection
```

In this case, the `person` object is no longer accessible because it's not referenced anywhere, so the garbage collector can free its memory.

**4. Finalization**

Just before an object's memory is reclaimed by the garbage collector, the garbage collector calls the object's `finalize()` method. This can be used to ensure an object finishes any important tasks before it is destroyed, such as closing open files.

**5. Memory leaks**

Even with automatic garbage collection, memory leaks can still occur in Java. A memory leak happens when an object that is no longer needed is still referenced somewhere, so the garbage collector can't reclaim its memory. Over time, this can lead to a significant amount of memory being used up, eventually causing the application to slow down or crash.

**6. Manual Memory Management**

Although Java handles most of the memory management internally, developers can still have some level of control and optimization over this process:

- Developers can manually make an object eligible for garbage collection by setting all references to it to `null`.

- Developers can also suggest to the JVM that it might be a good time to run the garbage collector by calling `System.gc()`. However, it's just a suggestion, and the JVM may choose to ignore it.

In summary, while Java abstracts much of the memory management process, understanding how it works helps you write more efficient code and avoid potential issues like memory leaks.