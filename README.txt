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

super.setSalary(this.hours*this.wage)  -- to set parent class variables using child class variables ( This can be done in child class only )

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

Have to override the method in abstract class.
Subclasses of abstract classes may or may not be abstract.
Abstract classes can have concrete methods.
Concrete subclasses of an abstract class must override all its abstract methods.

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

31/10/2021

24) Testing 

    @Test
    public void ageValidationTestValid() {
        Assert.assertTrue(new AgeValidation().isAgeValid(25));
    }

Testing of single small units of code such as a method or a class and asserting certain behavior is called unit testing. It is done by developers.
There are several frameworks available for automating unit tests. JUnit and TestNG are among the popular ones for Java.

JUnit is an open-source unit testing framework for Java. It provides classes to write and run automated tests. It provides

annotations to create and customize tests

test fixtures (to fix state) for setting up each test

assertions to test for expected results

test suites for grouping tests

Required JARs for JUnit: junit-4.12.jar, hamcrest-core-1.3.jar

The JUnit Runner is responsible for constructing the instances of the test classes before running the tests. 
It is also responsible for making them available for garbage collection after the tests.

The org.junit.Test annotation turns a public method into a test method.

A test method can either make assertions or expect exceptions.

Assertions are statements which claim a certain output from a module to be tested. They compare expected results with actual results.

If they match, the claim turns out to be true, and the test will pass.
Otherwise, the claim turns out false, and the test will fail.

The org.junit.Assert class is used for making assertions.

The Assert class provides static methods for testing a variety of conditions. These methods accept actual and expected results for comparison and determine whether a test method will pass or fail.

When a test fails, the test method throws an AssertionException. Optional error messages can be specified for Assertion exceptions. These exceptions are caught by JUnit and their messages are displayed.

What if we can create multiple test classes as a group to execute them together?

JUnit provides test suits to create groups of test classes so that the code maintainability is improved.

The following annotations are used for creating test suites:

@RunWith(Suite.class)
@Suite.SuiteClasses({UserTest.class, ProductTest.class, OrderTest.class})
public class TestSuiteDemo { ... }


Code coverage aims at determining the extent to which code is tested during unit testing.

With code coverage, you can determine the parts of the code which were not executed by test cases. You can then modify your unit tests to ensure those parts of the code are executed.

The larger the code coverage, better is the chance of having a bug-free code.

25) Exception Handling and Logging

i) Type Exception , Throw
An event occurring during the execution of a program and disrupting its normal flow is an exception.

Checked Exceptions - Cause compilation errors and prevent compilation. ( Can be handled by programmers )
UnChecked Exceptions - Cause runtime errors and abnormally terminate the programs.

The throw keyword is used to explicitly generate exceptional events. Any object of type Throwable can be thrown (We will see Throwable soon).

Exception e = new Exception();
throw e;

Also notice that we can pass a custom String message to the Exception constructor. This sets the message property of the exception and increases 
the usability of our applications.

throw new Exception(products[i].getName() + " out of stock");

All the exceptions belong to the Exception class, which is a child of the Throwable class.

String getMessage() - Returns the description of an exception
void printStackTrace() - Displays the stack trace ( used for debugging )
The throw keyword is used to explicitly mark an exceptional situation.

Location of the exception : package, class, method, filename and line number
Responding to the occurrence of an exception is called Exception Handling.

Whenever there is a chance of an exception to occur in a method, we have two choices:
 Handle the exception there itself
or
allow it to propagate to be handled somewhere else ( goes to the next class, next class and finally to the main class )

Checked Exception - something like compilation exceptions
Un Checked Exception - Runtime exceptions

Using try-catch blocks, we can handle exceptions in an effective way.

The code that can throw an exception is enclosed inside the try block. And a try block is immediately followed by one or more catch blocks or a finally block.

- A catch block is an exception handler which can handle the exception specified as its argument. A catch block can accept objects of type Throwable or its sub classes only.

-Whenever an exception is thrown inside a try block, it is immediately caught by the first matching catch block which can handle it. The code inside the try block 
following the line causing the exception is ignored.

-When an exception is caught and handled by a catch block, the execution continues from immediately after the try-catch block.

-If no matching catch block is found, the exception will remain unhandled and will be propagated.

-If no exception is thrown inside a try block, the catch blocks following it are ignored.

A catch block which can handle objects of Exception class can catch all the exceptions. 
This should always be the last catch block in the catch sequence.

In such situations, the finally block plays an important role.
It always executes, irrespective of whether an exception occurs or not.

The finally block will be disrupted if an exception occurs inside it, or if System.exit() is invoked before it.

ii) User defined Exception 

To make an application more flexible and manageable, Java allows us to have our own custom exceptions. 
This helps in working with specialized exceptions rather than a general one.

We can create a user-defined exception class by extending the Exception class:

class OutOfStockException extends Exception {
    public OutOfStockException(String productName) {
        super(productName);            // This string will be assigned to the message property of the exception 
    }
}

This exception denotes a more specific event (out of stock), and hence can be handled in a more specialized way.


26) Properties

To manage these user-friendly messages easily, it is a good practice to maintain them in a common place. One way to do this is to use a properties file.
Properties file is a text file used to store any kind of textual information in the form of key-value pairs.
It can be easily understood by a Java application with the help of the java.util.Properties class.

Properties files are usually used for

Standardization of messages (user friendly messages)

Configuration of enterprise applications

Internationalization or localization

To use the data from the properties file, we first need to read and load the properties file into a properties object. 
The properties object can then be used to get the message value by passing the corresponding key.

AppConfig.PROPERTIES.getProperty("OUT_OF_STOCK")
AppConfig is a utility class in the AppConfig.java file present in the resources package. 
This class has the code necessary for reading & loading key-value pairs from a properties file. Have a look at it.

In AppConfig.java, the following line opens the file for reading:
inputStream = AppConfig.class.getResourceAsStream("configuration.properties");
And the following loads the content into the static properties object:
PROPERTIES.load(inputStream);

Using the properties object, we can get a property value by specifying its key:
AppConfig.PROPERTIES.getProperty("OUT_OF_STOCK");

27 ) Testing on Exception

public class BillCalculatorTest {
    @Rule
    public ExpectedException ee = ExpectedException.none();        // Creating an empty rule
    
    @Test
    public void processOrderInvalidTest() throws Exception {
        Product[] products = new Product[1];
        products[0] = new Product("Jeans", 499, 0);                // Creating a product with zero stock
        
        ee.expect(OutOfStockException.class);                      // Expecting a type of exception
        ee.expectMessage("Jeans");                                 // Expecting a text in the exception message
        BillCalculator billCalc = new BillCalculator();
        billCalc.processOrder(products);
    }
}


*----------- You can use Java's instanceOf operator to check the type of an object --------------------*

Note: If a class implements multiple interfaces having the same default methods, it has to override them.
From the overridden methods, the default methods of a specified interface can be called using the super keyword.
E.g. MembershipCardHolder.super.addPointsFromFuelPurchase(500);

Note: A try block should be always followed by either at least one catch or a finally block.

Parent class exception should always be the last catch block.
Error is a subclass of Throwable. 
printStackTrace() helps the programmer to understand where the actual problem occurred. It helps to trace the exception.
