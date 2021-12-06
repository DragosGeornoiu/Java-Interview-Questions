### What is the difference between a class and an object?

An object is an instance of a class. The class is a blueprint of the object, defining its states and behavior.

When a class is created, no memory is allocated. Objects are allocated memory space whenever they are created.

The class has to be declared only once and it cannot be manipulated as it is not available in the memory.
An object is created many times as per requirement and each one can be manipulated.

Think of a class as Car and an object as BMW or Mercedes.

### What are the advantages of using packages?

Main two advantages are to avoid naming conflicts, meaning that there can be two classes with the name Student 
in two different packages, university.poli.Student and college.ace.Student, and to make easy searching or 
locating of classes.

### What is the purpose of using the "this" keyword in a class?
The "this" keyword is a reference variable that refers to the current object. It can be used to refer to current class 
properties such as instance methods, variable, constructors, etc.

### What is a constructor?
The constructor can be defined as the special type of method that is used to initialize the state of an object.
It is invoked when the class is instantiated, and the memory is allocated for the object. 
Every time, an object is created using the new keyword, the default constructor of the class is called. 
The constructor must not have an explicit return type.

### Does constructor return any value?
Not explicitly, but the constructor implicitly returns the current instance of the class.

### What is method overloading?
When a class has more than one method with same name but different parameters, then we call those methods are 
overloaded. Overloaded methods will have the same name but different number of arguments or different types of 
arguments.

### What is method signature? What are the things it consists of?
Method signature is used by the compiler to differentiate the methods. 
Method signature consist of three things.

1. Method name
2. Number of arguments
3. Types of arguments

### Can you make overloading by return type
No, compiler will give duplicate method error. Compiler checks only method signature for duplication not the return 
types. If two methods have same method signature, straight away it gives compile time error.

### If a method has four different overloaded forms, but all four different forms have different visibility(private, protected, public and default). Is “myMethod” properly overloaded?
Yes. Compiler checks only method signature for overloading of methods not the visibility of methods.

### What is the default constructor? When does Java create the default constructor and when does it not?
The default constructor is a no-args constructor which has no code inside it.
If you don’t implement any constructor in your class, the Java compiler inserts default constructor into your code on 
your behalf. You will not see the default constructor in your source code(the .java file) as it is inserted during compilation and present in the bytecode(.class file).

### What is the difference between default constructor and creating our own no-args constructor
Java won't provide a default constructor if you write any kind of constructor in class.
One difference between them is that the body of default constructor will always be empty whereas we can insert our 
own code in no-arg constructor.

### When do we need Constructor Overloading?
Sometimes there is a need of initializing an object in different ways. This can be done using constructor overloading.

### In which order are constructors from subclasses and superclasses loaded in the context of inheritance?
Order of execution of constructors in inheritance relationship is from top to bottom, from parent class(es) to child class(es).

### What is the purpose of using the "super" keyword or "super()" method in a class?
The super keyword in Java is a reference variable which is used to refer immediate parent class object.
1. super can be used to refer immediate parent class instance variable.
2. super can be used to invoke immediate parent class method.
3. super() can be used to invoke immediate parent class constructor

### What is Method Overloading and when do we need it?
If a class has multiple methods having same name but different in parameters, it is known as Method Overloading.
Method overloading increases the readability and reusability of the code. This provides flexibility to 
programmers so that they can call the same method for different types of data.

### What is Method Overriding and when do we need it?
The purpose of Method Overriding is that if the derived class wants to give its own implementation it can 
give by overriding the method of the parent class. When we call this overridden method, it will execute the
method of the child class, not the parent class.

### Name the 4 access modifiers and the behavior for each, especially in the context of inheritance
Modifier | Class | Package | Subclass | Global
--- | --- | --- | ---| ---
public | yes | yes | yes | yes
protected | yes | yes | yes | no
default | yes | yes | no | no
private | yes | no | no | no

### What are the differences between method overloading and method overriding
1. Method overloading is used to increase the readability of the program. Method overriding is used to provide the 
specific implementation of the method that is already provided by its superclass.
2. Method overloading is performed within class. Method overriding occurs in two classes that have an IS-A
(inheritance) relationship.
3. In case of method overloading, parameters must be different. In case of method overriding, parameters must be the same.
4. Method overloading is the example of compile time polymorphism. Method overriding is the example of run time polymorphism.
5. In Java, method overloading can't be performed by changing the return type of the method only. 
Return type can be the same or different in method overloading, but you must have to change the parameter. 
Return type must be same or covariant in method overriding.


### What is the difference between constructor initialization and inline field initialization
Field initialisers are executed before constructor bodies. (Which has implications if you have both 
initialisers and constructors, the constructor code executes second and overrides an 
initialised value)

Initialisers are good when you always need the same initial value but it can work in your favour or against you:
If you have many constructors that initialise variables differently (i.e. with different values), then initialisers 
are useless because the changes will be overridden, and wasteful.
On the other hand, if you have many constructors that initialise with the same value then you can save lines of code 
(and make your code slightly more maintainable) by keeping initialisation in one place.

### What is variable hiding/shadowing?
A variable is shadowed if there is another variable with the same name that is closer in scope.

A class can declare a variable with the same name as an inherited variable from its parent class, 
thus "hiding" or shadowing the inherited version.

### Are constructors inherited?
No. Because constructing your subclass object may be done in a different way from how your 
superclass is constructed. You may not want clients of the subclass to be able to call certain 
constructors available in the superclass.

### What is constructor chaining?
Constructor chaining is the process of calling one constructor from another constructor with respect to current object.

Constructor chaining can be done in two ways:
1. Within same class: It can be done using this() keyword for constructors in same class
2. From base class: by using super() keyword to call constructor from the base class.

### Which class is the superclass for all the classes?
The Object class.

### Why is multiple inheritance not supported in java?

Main reason why the Java programming language does not permit you to extend more than one class is to avoid the 
issues of multiple inheritance of state, which is the ability to inherit fields from multiple classes (diamond problem).

If multiple inheritance is allowed then when you create an object by instantiating that class, that object will 
inherit fields from all the class's superclasses. It will cause two issues.
1. What if methods or constructors from different super classes instantiate the same field?
2. Which method or constructor will take precedence?