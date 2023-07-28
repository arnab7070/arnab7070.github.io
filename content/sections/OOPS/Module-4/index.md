---
title: "Module 4"
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

## Example of commands as methods and as objects in Java
- To illustrate how to implement commands as methods and as objects in Java, let's create a simple example of a text file application that can perform operations such as opening, saving, and writing to a text file.
- We will create a TextFile class that represents the receiver of the commands. It will have two fields: name and content. It will also have three methods: open, save, and write. These methods will print some messages to the console to simulate the file operations.

```java
// Receiver class
public class TextFile {
    private String name;
    private String content;

    // constructor
    public TextFile(String name) {
        this.name = name;
        this.content = "";
    }

    // methods to perform file operations
    public void open() {
        System.out.println("Opening file " + name);
    }

    public void save() {
        System.out.println("Saving file " + name);
    }

    public void write(String text) {
        content += text;
        System.out.println("Writing " + text + " to file " + name);
    }
}
```

- To implement commands as methods, we will create a TextFileOperation interface that defines the command's API. It will have one abstract method: execute. This method will take no parameters and return a String value.

```java
// Command interface
@FunctionalInterface
public interface TextFileOperation {
    String execute();
}
```

- To implement commands as objects, we will create three classes that implement the TextFileOperation interface: OpenTextFileOperation, SaveTextFileOperation, and WriteTextFileOperation. These classes will have one field: textFile. They will also have constructors that take a TextFile object as a parameter and assign it to the field. They will also override the execute method to invoke the corresponding method on the textFile object and return a String value.

```java
// Command implementations
public class OpenTextFileOperation implements TextFileOperation {
    private TextFile textFile;

    // constructor
    public OpenTextFileOperation(TextFile textFile) {
        this.textFile = textFile;
    }

    // override execute method
    @Override
    public String execute() {
        textFile.open();
        return "Opened file " + textFile.getName();
    }
}

public class SaveTextFileOperation implements TextFileOperation {
    private TextFile textFile;

    // constructor
    public SaveTextFileOperation(TextFile textFile) {
        this.textFile = textFile;
    }

    // override execute method
    @Override
    public String execute() {
        textFile.save();
        return "Saved file " + textFile.getName();
    }
}

public class WriteTextFileOperation implements TextFileOperation {
    private TextFile textFile;
    private String text;

    // constructor
    public WriteTextFileOperation(TextFile textFile, String text) {
        this.textFile = textFile;
        this.text = text;
    }

    // override execute method
    @Override
    public String execute() {
        textFile.write(text);
        return "Wrote " + text + " to file " + textFile.getName();
    }
}
```

- To test our commands as methods and as objects, we will create a Main class that creates a TextFile object and invokes its methods directly or through command objects.

```java
// Main class
public class Main {
    public static void main(String[] args) {
        // create a text file object
        TextFile textFile = new TextFile("test.txt");

        // invoke file operations directly using methods
        System.out.println("Using methods:");
        textFile.open();
        textFile.write("Hello world");
        textFile.save();

        // invoke file operations indirectly using command objects
        System.out.println("Using commands:");
        TextFileOperation openCommand = new OpenText
    }
}
```