## What is SOLID?

In software engineering, SOLID is a acronym for five design principles intended to make object-oriented 
designs more understandable, flexible, and maintainable. The principles are a subset of many principles 
promoted by American software engineer and instructor Robert C. Martin

The Principles are:

* **S**ingle-responsibility principle 
* **O**pen–closed principle
* **L**iskov substitution principle
* **I**nterface segregation principle
* **D**ependency inversion principle

## Single responsibility principle

Every class, module, or function in a program should have one responsibility/purpose in a program. 
Another way this principle is described is: every class should have only one reason to change.

This principle is helpful to avoid having large classes or methods, which are doing more than you would 
expect them to. A good trick to finding out if the method or class is doing more than it should is to
try to describe its behavior, if you find yourself using the word "and" it probably needs to be split.

For example: if you have a method named saveTotalPriceInDatabase(pricePerDay: BigDecimal, noOfDays: int) 
which has responsibility of calculating the total price by multiplying the two inputs, pricePerDay x noOfDays,
and save the result to the database, you can already see that we had to use the word "and" when describing
the behavior of this method. Though a basic example, this is a violation of the Single Responsibility 
Principle.

The previous example was for a method violating the SRP principle, but the principle applies to classes,
modules and even microservices.

To mention that a single responsibility does not translate to single method classes, it just means a single 
reason for existence.

The SRP Principle is the first step in writing simple, readable and easily modifiable code.

## Open-close principle

The open–closed principle states that methods, classes, modules etc. should be open for extension, but 
closed for modification. That means that the entities can allow their behaviour to be extended without
modifying its source code.

To fully grasp this principle you have to think a little of people who consume your code (be it a 
method, a class, a module or an API) as customers, not as members of the same team.
For example, let's say you have a Person Class with two fields, age and name.

```java
public class Person {
    int age;
    String name;
}
``` 

If you afterwards want a person to also have an employee Id, you would have to add a new field in your Person
class. But in order too fully adhere to the Open-Close Principle, your Person class should be closed for modifications,
so what you would have to do is to create a new Employee class which extends the Person class

```java
public class Employee extends Person {
    String empID;
}
``` 

Now, let's say you find out that you want to have an address for your Employer, in order to respect
the Open-Close Principle, you would have to create a new class named EmployeeWithAddress (maybe with a better
naming).

```java
public class EmployeeWithAddress extends Employee {
    private String address;
}
``` 

And that is how you would fully respect the Open-Closed Principle. You probably think this is not a good approach, since you could
just rewrite your Person class and have the address inside it, and in most cases you would actually
be right. If the class is consumed (or used) in places you or your team can also modify, it would 
be a better approach to just modify it. Remember that these principles are a guideline, including the
Open-Close Principle, not something to follow blindly.

I said earlier to think of who consumes your classes. If the project containing your initial Person
class is built as a jar and now used throughout an entire organization with different teams as a 
dependency, and it might be the case that they themselves extended it already and adapted it to their
needs, if you would directly modify the Person class, all the teams which consume it (or use it) will
now have to adapt to your change. 
In that case, respecting the Open-Close Principle should be a must.


## Liskov substitution principle

Liskov Substitution Principle (LSP) states that objects of a superclass should be replaceable with objects of its 
subclasses without breaking the application.

In other words, what we want is to have the objects of our subclasses behaving the same way as the objects of our 
superclass.

It is based on the concept of "substitutability" – a principle in object-oriented programming stating that an 
object (such as a class) and a sub-object (such as a class that extends the first class) must be interchangeable 
without breaking the program

Let's think of the following hierarchy. You have a bird base class which contains a fly method.
We will only have a print in the method, but think as this method would contain the actual action of flying.

```java
public class Bird {
    public void fly(){ System.out.println("Bird is flying"); }
}
```

If we need to specify also a Duck class, since a Duck is a bird, we will extend the Bird class:

```java
public class Duck extends Bird {
    @Override
    public void fly(){ System.out.println("Duck is flying"); }
}
```

But what if we need an Ostrich class in our project? The issue is that the ostriches do not fly, so in most cases
we will have to maybe throw an exception in case the fly() method of Ostrich class is called.

```java
public class Ostrich extends Bird {
    @Override
    public void fly(){ throw new UnsupportedOperationException("Ostriches cannot fly."); }
}
```

But here is the issue, there could, and probably should, be cases where the Ostrich class is upcasted as a Bird class.
Or even more, it can appear in a List<Bird> which calls at some point the fly method.
The issue is that someone who would use the Bird class and call the fly() method on it would not expect any 
circumstances in which that would not work, since at a first taught all birds fly and since the fly method is clearly
in the Bird class, that expectancy is quite reasonable.

How would we resolve it? In this case quite simple. If the fly() method is present in the Bird class, then all children
of Bird class should be able to fly. When we need to create the Ostrich class, we need to think that it cannot be a 
Bird since birds need to fly and an Ostrich is not able to do that. 
We either leave it as a standalone class or create two new abstractions as FlyingBird, from which Duck can extend, and 
a NonflyingBird class, from which an Ostrich (and other maybe in the future?) can extend from.

There is no easy way to enforce this principle. The compiler only checks the structural rules defined by the Java 
language, but it can’t enforce a specific behavior. The programmer is in charge of ensuring this principle is followed. 

A good saying regarding this principle is the following: "If it Looks Like a Duck, Quacks Like a Duck, But Needs 
Batteries - You Have the Wrong Abstraction"

## Interface segregation principle

Interface segregation principle (ISP) states that no code should be forced to depend on methods it does not use.
The principle favors writing small interfaces, with a few method, instead of large interfaces; this will
allow you to use more appropriate interfaces to your use case, instead of having to use a large interface
which will make you implement methods you do not need or want.

I am going to reuse the previous example. Let's say you start designing your Bird interface
```java
public interface Bird {
    void searchForFood();
    void eat();
    void fly();
    void sing();
    void getName();
    void getLatinName();
}
```

When this interface was designed, it suited your every need, butut it is quite bloated. Again,
if we need an Ostrich class, the fly() method is useless to an ostrich. But because we have this
big interface which wants to cover every scenario, we would be forced to implement the fly() method.
Also, many other bird species do not sign, but will be forced to implement the sing() method.

The solution, as was for the Liskov Substitution Principle, is to have smaller interfaces

```java
public interface Bird {
    void getName();
    void getLatinName();
}

public interface EatingBird {
    void searchForFood();
    void eat();
}

public interface FlyingBird {
    void fly();
}

public interface SingingBird {
    void sing();
}
```

Because we have split the interfaces by functionality we can now easily implement a JavaSparrow, which
uses all our small interfaces, but we can also implement easily an Ostrich class, which just will
not implement the FlyingBird and Singing Bird. If we want to implement a RobotBird, which will not 
eat, we do not implement the EatingBird interface. 

```java
public class JavaSparrow implements Bird, EatingBird, FlyingBird, SingingBird {
    //implementation of method
}

public class Ostrich implements Bird, EatingBird {
    //implementation of method
}

public class RobotBird implements Bird, FlyingBird, SingingBird {
    //implementation of method
}
```


## Dependency Inversion

This is probably the most complicated of the principles, so let's start with the definition:

High-level modules should not depend on low-level modules; both should depend on abstractions. 
Abstractions should not depend on details. Details should depend upon abstractions.

Other definitions you will find can look something like this:
1. High-level modules should not import anything from low-level modules. Both should depend on abstractions (e.g., interfaces).
2. Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

Why do we want to not have a tight coupling between two modules? 
A tightly coupled system usually implies that a change in one module will have a ripple effect of changes in other 
modules that depend on the modified module. Another negative is that a module might become difficult to reuse and test, 
because its dependent modules must be included.

The name of the principle is a little confusing, as the design principle does not just change the direction of the 
dependency. It splits the dependency between the high-level and low-level modules by introducing an abstraction between 
them. 
So instead of the having a single dependency from the high-level module to the low level module you get two dependencies:
1. the high-level module depends on the abstraction, and
2. the low-level depends on the same abstraction.

Because of this, we can rewrite the principle as:
1. High-level modules should not import anything from low-level modules; they should both depend on abstractions.
2. Abstractions should not depend on concrete implementations; concrete implementations should depend on abstractions