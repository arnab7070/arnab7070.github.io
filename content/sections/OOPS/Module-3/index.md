---
title: "Inheritance in JAVA"
date: 2023-07-27T07:15:40+05:30
draft: false
image: module3.png
description: This tutorial covers Inheritance in Java, introduces classifications of Design Patterns (Creational, Structural, Behavioral), and explains the Iterator Pattern. It features code snippets illustrating inheritance and the use of the Iterator Pattern for sequential access in collections.
---

# Inheritance

Inheritance is a fundamental concept in OO design where a class is based on another class, absorbing its attributes and behaviors and enhancing them. Inheritance allows programmers to create classes that are built upon existing classes, enabling code reusability and the addition of new features to existing code.

```java
// A base class
class Animal {
    void eat() {
        System.out.println("Animal is eating...");
    }
}

// A derived class
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking...");
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // from Animal class
        dog.bark(); // from Dog class
    }
}
```

In the above example, `Dog` is a derived class that inherits from the `Animal` base class. A `Dog` object can access the `eat` method of `Animal` and its own `bark` method.

# Design Patterns

Design patterns are typical solutions to commonly occurring problems in software design. They represent the best practices used by experienced software developers. Design patterns are categorized into three groups: Creational, Structural, and Behavioral.

1. **Creational Patterns**: Provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using a constructor. This gives the program more flexibility in deciding which objects need to be created for a given use case. Examples: Factory Method, Abstract Factory, Builder, Prototype, Singleton.

2. **Structural Patterns**: Concerned with class and object composition. They provide a manner to define relationships between classes or objects so that if one part changes, the impact on the overall structure will be minimal. Examples: Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.

3. **Behavioral Patterns**: Concerned with the interaction and responsibility of objects. In other words, they focus on the communication between objects. Examples: Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor.


# Iterator Pattern

The Iterator Pattern is a behavioral design pattern that provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation. It involves two key components: 

1. **Iterator**: The 'Iterator' defines an interface for accessing and traversing elements.
2. **Concrete Iterator**: The 'ConcreteIterator' implements the 'Iterator' interface and keeps track of the current position in the traversal of the aggregate.

Here is an example of how to use the Iterator Pattern in Java:

```java
import java.util.Iterator;
import java.util.ArrayList;

class Main {
    public static void main(String[] args) {
        ArrayList<String> animals = new ArrayList<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Horse");

        Iterator<String> it = animals.iterator();
        while(it.hasNext()) {
            System.out.println(it.next());
        }
    }
}
```

In this code, `ArrayList` is the aggregate object and the `Iterator` object `it` is used to traverse through the elements. The `hasNext` method of the iterator object is used to ensure there is a next element, and the `next` method is used to move to the next element in the list.

In your examination, understanding these concepts and being able to provide code examples will demonstrate your grasp of OO design and the use of design patterns in Java.


