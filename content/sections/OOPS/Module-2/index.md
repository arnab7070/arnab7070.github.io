---
title: "Encapsulation, Polymorphism"
date: 2023-07-25T20:37:06+05:30
draft: false
image: module2.png
description: This tutorial will teach you the four main features of object-oriented programming, encapsulation, object identity, polymorphism, and inheritance, with examples in Java. So without wasting any time let's dive into the main content of our topic.
---

# Object-Oriented Programming Tutorial

Object-oriented programming (OOP) is a programming paradigm that organizes data and behavior into reusable units called **objects**. Objects have **attributes** (data) and **methods** (functions) that operate on the data. Objects can also interact with other objects through **messages**.

OOP has four main features: **encapsulation**, **object identity**, **polymorphism**, and **inheritance**. Let's see what they mean and how they work.

## Encapsulation

Encapsulation is the principle of hiding the internal details of an object from the outside world. It means that only the object itself knows how to manipulate its data and behavior, and other objects can only access it through a well-defined interface.

Encapsulation helps to achieve **data abstraction**, which is the process of providing only the essential information about an object to the users, while hiding the implementation details.

Encapsulation also helps to achieve **data integrity**, which is the property of ensuring that the data is valid and consistent. By restricting the access and modification of the data to the object's methods, we can prevent unauthorized or invalid changes to the data.

For example, suppose we have a class called `BankAccount` that represents a bank account with a balance attribute and a withdraw method. We can use encapsulation to make the balance attribute private, so that only the withdraw method can access and modify it. This way, we can ensure that the balance is always positive and accurate, and no other object can tamper with it.

```java
public class BankAccount {
  // private attribute
  private double balance;

  // public constructor
  public BankAccount(double initialBalance) {
    // check if initial balance is positive
    if (initialBalance >= 0) {
      balance = initialBalance;
    } else {
      balance = 0;
    }
  }

  // public method
  public void withdraw(double amount) {
    // check if amount is positive and less than or equal to balance
    if (amount > 0 && amount <= balance) {
      balance = balance - amount;
    } else {
      System.out.println("Invalid withdrawal amount");
    }
  }

  // public method
  public double getBalance() {
    return balance;
  }
}
```

To access or modify the balance of a bank account object, we have to use its methods, such as `getBalance` or `withdraw`. We cannot directly access or modify its private attribute, such as `balance`.

```java
// create a bank account object with an initial balance of 1000
BankAccount myAccount = new BankAccount(1000);

// print the balance using the getBalance method
System.out.println("My balance is " + myAccount.getBalance());

// try to withdraw 500 using the withdraw method
myAccount.withdraw(500);

// print the new balance using the getBalance method
System.out.println("My new balance is " + myAccount.getBalance());

// try to withdraw 1000 using the withdraw method
myAccount.withdraw(1000);

// print the new balance using the getBalance method
System.out.println("My new balance is " + myAccount.getBalance());

// try to access or modify the private attribute directly
myAccount.balance = -100; // error: cannot access private attribute
```

Output:

```
My balance is 1000.0
My new balance is 500.0
Invalid withdrawal amount
My new balance is 500.0
error: cannot access private attribute
```

## Object Identity

Object identity is the principle of distinguishing different objects from each other based on their unique identifiers. It means that each object has a unique identity that does not depend on its attributes or methods.

Object identity helps to achieve **object equality**, which is the property of comparing two objects based on their identities, not their values. By using object identity, we can determine if two objects are the same or different, regardless of their attributes or methods.

For example, suppose we have two bank account objects with the same balance attribute, but different identifiers. We can use object identity to compare them and see that they are not equal, even though they have the same value.

```java
// create two bank account objects with the same initial balance of 1000
BankAccount account1 = new BankAccount(1000);
BankAccount account2 = new BankAccount(1000);

// print their balances using the getBalance method
System.out.println("Account1 balance is " + account1.getBalance());
System.out.println("Account2 balance is " + account2.getBalance());

// compare them using object identity (== operator)
System.out.println("Are they equal? " + (account1 == account2));
```

Output:

```
Account1 balance is 1000.0
Account2 balance is 1000.0
Are they equal? false
```

## Polymorphism

Polymorphism is the principle of allowing an object to behave differently depending on the context. It means that an object can have different forms or types, and can perform different actions based on its form or type.

Polymorphism helps to achieve **dynamic binding**, which is the process of determining the type and behavior of an object at run time, not at compile time. By using polymorphism, we can make our code more flexible and adaptable to different situations.

There are two types of polymorphism: **static** and **dynamic**. Static polymorphism is achieved by **overloading**, which is the process of defining multiple methods with the same name but different parameters. Dynamic polymorphism is achieved by **overriding**, which is the process of redefining a method in a subclass that was already defined in a superclass.

For example, suppose we have a class called `Animal` that represents an animal with a name attribute and a speak method. We can use static polymorphism to overload the speak method with different parameters, such as the number of times or the volume. We can also use dynamic polymorphism to override the speak method in subclasses that represent specific animals, such as `Dog` or `Cat`.

```java
public class Animal {
  // protected attribute
  protected String name;

  // public constructor
  public Animal(String name) {
    this.name = name;
  }

  // public method (static polymorphism)
  public void speak() {
    System.out.println("I am an animal");
  }

  // public method (static polymorphism)
  public void speak(int times) {
    for (int i = 0; i < times; i++) {
      speak();
    }
  }

  // public method (static polymorphism)
  public void speak(String volume) {
    System.out.println("I am an animal (" + volume + ")");
  }
}

public class Dog extends Animal {
  // public constructor
  public Dog(String name) {
    super(name);
  }

  // public method (dynamic polymorphism)
  @Override
  public void speak() {
    System.out.println("Woof! I am " + name);
  }
}

public class Cat extends Animal {
  // public constructor
  public Cat(String name) {
    super(name);
  }

  // public method (dynamic polymorphism)
  @Override
  public void speak() {
    System.out.println("Meow! I am " + name);
  }
}
```

To use polymorphism, we can create objects of different types and assign them to a common reference type, such as `Animal`. Then, we can call the same method on the reference type, and see that it behaves differently based on the actual type of the object.

```java
// create an animal object with the name "Bob"
Animal animal = new Animal("Bob");

// create a dog object with the name "Rex"
Dog dog = new Dog("Rex");

// create a cat object with the name "Lily"
Cat cat = new Cat("Lily");

// assign them to a common reference type
Animal[] animals = {animal, dog, cat};

// call the same method on each reference type
for (Animal a : animals) {
  a.speak();
}

// call the overloaded method on each reference type
for (Animal a : animals) {
  a.speak(2);
}

// call the overloaded method on each reference type
for (Animal a : animals) {
  a.speak("loudly");
}
```

Output:

```
I am an animal
Woof! I am Rex
Meow! I am Lily
I am an animal
I am an animal
Woof! I am Rex
Woof! I am Rex
Meow! I am Lily
Meow! I am Lily
I am an animal (loudly)
Woof! I am Rex (loudly)
Meow! I am Lily (loudly)
```