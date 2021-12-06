### What is abstraction?
Abstraction in Java is a technique by which we can hide the data that is not required to users. It hides all unwanted 
data so that users can work only with the required data.

### How to achieve or implement Abstraction in Java?
There are two ways to implement abstraction in Java:
1. Abstract class (0 to 100%)
2. Interface (100%)

### What is the difference between abstract class and concrete class?
There are mainly two differences between an abstract class and concrete class:
1. We cannot create an object of abstract class. Only objects of its non-abstract (or concrete) subclasses can 
be created.
2. An abstract class can have zero or more abstract methods that are not allowed in a non-abstract class 
(concrete class).

### What is an abstract method in Java?
A method which is declared with abstract modifier and has no implementation, no body, it is called an abstract 
method in Java.

### Can an abstract method be declared with private modifier?
No, it cannot be private because the abstract method must be implemented in the child class.

### When to use Abstract method in Java?
1. When the same method has to perform different tasks depending on the object calling it.
2. When you need to be overridden in its non-abstract subclasses.

### Why abstract class have a constructor even though you cannot create object?
We cannot create an object of abstract class, but we can create an object of subclass of abstract class. 
When we create an object of subclass of an abstract class, it calls the constructor of subclass.

If the abstract class wouldn't have constructor, a class that extends that abstract class will not get compiled.

### Can abstract class be final in Java?
No, abstract class can not be final in Java. Making them final will stop abstract class from being extended, 
which is the only way to use abstract class.

### What is an interface in Java?
An interface in Java is a mechanism that is used to achieve complete abstraction. 
It is basically a kind of class that contains only constants and abstract methods.

### Can an interface extends another interface in Java?
Yes, an interface can extend another interface.

### Can an interface be final?
No. Doing so will result compilation error.

### Why an interface cannot have a constructor?
Inside an interface, a constructor cannot be called using super keyword with hierarchy.

###Why an Interface can extend more than one Interface but a Class can’t extend more than one Class?
We know that Java doesn't allow multiple inheritance, but an Interface is a pure abstraction model. 
It does not have inheritance hierarchy like classes, therefore, an interface is allowed to extend more than 
one interface.

### What is the use of interface in Java?
There are many reasons to use interface in java. They are as follows:
1. An interface is used to achieve fully abstraction.
2. Using interfaces is the best way to expose our project’s API to some other project.
3. Programmers use interface to customize features of software differently for different objects.
4. By using interface, we can achieve the functionality of multiple inheritance.

### Is it necessary to implement all abstract methods of an interface (or an abstract class)?
Yes, all the abstract methods defined in interface must be implemented if the current class is a concrete class.

### Can we reduce the visibility of interface method while overriding?
No, while overriding any interface methods, we must use public only. This is because all interface methods are 
public by default. We cannot reduce the visibility while overriding them.

### If same method is defined in two interfaces can we override this method in class implementing these interfaces?
Yes, implementing the method once is enough in class. 
A class cannot implement two interfaces that have methods with same name but different return type.

### Can we declare an Interface with “abstract” keyword?
Yes, we can declare an interface with “abstract” keyword. 
But, there is no need to write like that. All interfaces in java are abstract by default.

### Like classes, do interfaces also extend Object class by default?
No. Interfaces don’t extend Object class.

### What is interface default method in java 8?
Before Java 8, the interface only contains method signatures. 
With Java 8 new feature Default Methods or Defender Methods, you can include method body within the interface.
All you need to do is add "default" keyword in front of the implementation method with in the interface. 
This is the new way of declaring the method body in Java 8 for an interface, default methods comes along with implementation.

### Why do we need to implement a method within the interface?
Let's say you have an interface which has multiple methods, and multiple classes are implementing this interface. 
One of the method implementation can be common across the class, we can make that method as a default method, 
so that the implementation is common for all classes.

### Can an interface contain more than one Default method?
Yes, any Java interface can contain more than one default method.

### What happens if a concrete class implements two interfaces which have a default method with the same signature



