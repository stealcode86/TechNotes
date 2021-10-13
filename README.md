# TechNotes


8/4/2021


1) Rules for naming identifiers:
case sensitive

should not start with a number

should start with a letter, $ or _

should not have spaces

should not be a Java keyword or a literal

no restriction on length

2) Syntax:  <data type> <identifier> = <value>;

3) Arithmetic Operators (+, -, *, /, %, ++, --)

Bitwise Logical Operators (&, |, ^, ~, <<, >>, >>>)

Relational Operators (==, !=, <, <=, >, >=)

Assignment Operators (=, +=, -=, *=, /=, %=)

Short-Circuit Logical Operators (&&, ||, !)

Ternary Operator: It is a short form of if-then-else statement
Syntax:  <condition> ? <statement if true> : <statement if false>;

4) long regId = 4567L;
int iRegId = (int)regId;    // Explicit Type Casting


------------Classes

5) class Product {
    ( Access specifier ) private int productId;
}

 public float ( Return type ) getPriceAfterDiscount(int discountPercentage ( Formal argument/ parameters ) ) - Method {
 ( Local variable )float discountedPrice = price - (price * discountPercentage / 100);
        return discountedPrice;
    }

public static int add(int x, int y ( actual arguments ) )

6) Object 

An object is an instance of a class.

It allows us to use the attributes and methods specified in the class

A class can have any number of objects

An object holds data related to an instance of a class

13/8/2021

7) Method Overloading ( Method return type and name will be same )


The displayDetails() method actually has two versions. One which shows all the details for E-Mart employees, and the other which shows the name, 
discounted price and stock availability for the customers.

This is called method overloading. It allows having different implementations of the same behavior depending upon the arguments.

8) Constructor

A constructor is a special method which has the same name as the class and no return type. It is used for creating objects and initializing them with values.

A class can have multiple constructors to initialize different number of fields. This is called constructor overloading.

9) This is called encapsulation, the bundling of data and related methods into a single unit.
This allows restricting access to the members.

The data members (attributes) are usually private to prevent direct access to them

Methods (behaviors) are usually public to be accessible from outside the class

10)  Abstraction ---  float finalPrice = prodObj.getPriceAfterDiscount(15);

11) Java has its memory logically divided into two primary sections - Stack and Heap.

All local variables and method invocations are stored in the stack

All objects along with their instance variables are stored in the heap

When an object does not have any reference, it becomes eligible for garbage collection.

11) Static 


Hence, a static context, i.e. static blocks and static methods, cannot access non-static (instance) members directly.

However, non-static methods can access static members.

Yes, static blocks are always executed whenever the class is defined, and since class gets defined only once, 
the static blocks also get executed only once.
The static attributes are created during the defining of the class and not the instancing of it. Hence before the object creation also, 
the static elements can be accessed.
Can a static element access a non-static attribute? Since the existence of a non-static attribute is not defined during the execution of the static block, 
the static block cannot access any non-static elements

12) Inheritance 

When an object is based on another object, i.e. acquires characteristics and behaviors from another object, the relationship is that of inheritance.

Inheritance or "is-a" relationship exhibits the concept of reusability through a valid relationship between any two real world objects.
Example: A premium customer is a customer, a project manager is an employee, a car is an automobile.
If we want to invoke a parameterized constructor of the parent class, we need to pass the required parameters in the super keyword.
Also, the call to a super constructor has to be the first statement inside a constructor.
The orderProducts() method in the parent class calculates and returns the total bill amount. 
Since the overridden methods in the child classes need to get the total bill amount before performing their own operations, they first call the parent's method.

@Override is done when we want to specifically get value of a class using the method of parent class.

13) Super 

Actually, the super keyword can be used to refer to any non-private members of a parent in a hierarchy. This facilitates reusability of existing functionalities.

Apart from accessing the parent class constructors and methods which have been overridden in the child class, super keyword can also be used to access instance 
variables (non-private) of the parent class when both the parent and child classes have variables with the same name.

The display() method in A cannot be directly called from an instance method in C. ( C--B--A )
The super() call should be the first line always

If parent constructor has a parameter, super() must be invoked in child class else not required.

super.setSalary(this.hours*this.wage)  -- to set parent class variables using child class variables 

14) Aggregation 

We can see that address variable is an object of Address class.

When an object contains another object as its attribute, we have an aggregation between them. It is termed as "has-a" relationship.

15) When an object utilizes another object in order to perform its activities, a relationship of association is established between them. This is termed as "uses-a" relationship.

Example: A customer uses products and bill calculator to process orders, a driver uses a car to travel

16) Method Overriding 

We can see that although RegularCustomer and PremiumCustomer inherit the orderProducts() method from Customer, they define it again with a modified implementation.

This is called method overriding.

Method overriding lets you redefine a method in the child class which is already present in the parent class.

A few things to note while overriding methods:

When we override a method in the child class, it should have the same signature as that of the parent class

It should not have a weaker access privilege (will be discussed soon)

Private methods are not inherited, hence not overridden.

Static methods are not overridden. They will be called based on the type of reference used.

17) Packages

The package keyword is used to specify the package of a class. It should be the first line of a java file. To use a class from another package, the import keyword is used.

The naming convention for packages is lowercase

Only public classes can be imported into different packages

public - accessible everywhere (4)
private - accessible inside its own class (1)
protected - accessible inside the same package and to the sub classes in different packages (3)
default - accessible inside the same package  (2)

18) Final 

The final keyword is generally used with components which should never change, i.e. remain constant.
It is used to restrict modification of variables, overriding methods and inheriting classes.
Some examples of final classes from the Java library are String and Wrapper classes. The final keyword can be used with variables, classes and methods:
final field value cant be changed, final method cant be overridden, in sub classes, final class cant be sub classed.
Option Compilation error is Correct

Final field names cannot be assigned ( for eg: final String name; )

"Final class " does not allow any sub-classes

19) Abstract keyword

Since the above method is abstract, the class itself becomes incomplete. And there is a need for extending this class to complete it. To enforce this, the abstract keyword is used with the class.

Any class extending the abstract class must provide the missing implementation to complete it:

@Override
    public void displayDetails()

Have to override the method in abstract class
Subclasses of abstract classes may or may not be abstract
Abstract classes can have concrete methods
Concrete subclasses of an abstract class must override all its abstract methods

The abstract keyword signifies that something is not complete. It can be used with classes and methods.
We use the abstract keyword when:

We do not have the complete implementation of methods and classes
We do not want a class to be instantiated
An abstract method is a method without any definition, i.e. the body.
If a class contains at least one abstract method, the class should be abstract

Abstract classes enforce inheritance

and

Abstract methods enforce overriding

And we get another flavour of dynamic binding


20) Interface

This is an interface. As you can see, it specifies the behaviors by declaring methods, but doesn't provide the implementations ( no logic , just method name ).

Using interfaces we specify what is to be done, without telling how.
The how is then implemented by the classes which follow the specifications:

The PremiumCustomer class which implements the MembershipCardHolder interface has to override and provide the implementations of the methods from the interface.
--An interface is used to define a generic template which can be implemented by various classes.
The implements keyword is used to implement an interface. The classes implementing an interface must implement all the specified methods. Otherwise, they should be made abstract

All methods present in interface ( InterfaceDemo )
public abstract void displayName(); -- obj.displayName(); ( method is present in Obj class )
default void displayCountry()      -- obj.displayCountry(); ( method not present in Obj class ) ( Cant modify the method in Obj class )
public static void displayCompany() InterfaceDemo.displayCompany(); ( Can have the same method in Obj class and modify it )

Abstract class can implement interface 

"SavingsAccount extends Account" is correct if both Account and SavingsAccount are either interfaces or classes

21) Variable Arguments 

public float orderProducts(Product... products) {
    // Statements
}

float totalAmount = regCust.orderProducts(halfPant, trousers);          // Passing variable arguments; Creating arrays to pass is not required
    }


This is called varargs. It is a construct that allows methods to accept zero or more arguments. It internally uses arrays to process the variable number of arguments

It is better than overloading as it can take zero or 'n' number of arguments. It is convenient to use as we don't have to create arrays of arguments to pass to the methods.

There can be only one varargs argument in a method. If present, varargs must be the last parameter

22) Summary 

Abstraction - the process of exposing the relevant details
e.g. The dashboard of a car is exposed to the driver
 

Encapsulation - the process of restricting access to the members
e.g. The internals of a switchboard are hidden from the users
 

Inheritance - a technique to create specialized classifications from a general one
e.g. Homo sapians are animals
 

Polymorphism - an object's ability to behave differently depending upon the context
e.g. A phone can behave like a camera, video player, gaming console, etc.

23) Code Analysis

PMD is a source code analyzer, which checks code against a predefined set of rules.

1. Unused imports should not be present

2. System.out.println() statements should not be present

3. Variable naming convention should be followed
    - variable names should be in camel case

4. Method naming convention should be followed
    - method names should be in camel case

5. Class naming convention should be followed
    - class names should be in pascal case

6. Package naming convention should be followed
    - package names should be in lowercase

7. printStackTrace() should not be present


*----------- You can use Java's instanceOf operator to check the type of an object --------------------*

Note: If a class implements multiple interfaces having the same default methods, it has to override them.
From the overridden methods, the default methods of a specified interface can be called using the super keyword.
E.g. MembershipCardHolder.super.addPointsFromFuelPurchase(500);
