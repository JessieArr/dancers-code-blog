---
title: "Commonly Misused Programming Terms"
date: "2018-07-25"
---

One big challenge I often see new programmers struggle with early in their careers is that they often don’t know the correct vocabulary to describe the things they deal with in code.  As a result, often times a lot gets lost in communication when they misuse words while talking to senior programmers, because they are effectively describing something different from what they mean.

A few years into my career, I noticed that I was using certain words interchangeably when describing things without really understanding the difference between them. So I started trying to research each term I felt I didn’t fully understand and get into the habit of using it correctly as much as possible.

As I began to learn the difference between various terms, I realized something: the senior programmers on my team always used terminology correctly, while junior programmers did not. Furthermore, the junior programmers were often inadvertently describing things that were either nonsensical or simply wrong by accidentally using the wrong words to describe the code constructs they saw. While it is often possible for people to infer your intention from the context of what you’re describing, it is worth making an effort to use the most correct terminology possible so that you can avoid the possibility miscommunication with your fellow programmers.

This blog will be a quick overview of a few terms which I commonly hear misused or misunderstood by junior programmers, in the hopes of helping people communicate themselves more effectively to their coworkers! The terms will mostly be ones relevant to modern Object-Oriented Programming, and I’ll include code examples in C#, but I think that you will find that there is a lot of cross-over between various languages.

**Field versus Property:**

The following code example defines one Field and two Properties:

![devenv_2016-02-22_21-01-01](images/devenv_2016-02-22_21-01-01.png)

Fields are local values defined on a class which, when on the left-hand side of an assignment statement, do not execute any logic, as they have no concept of a getter or setter. Properties, on the other hand, execute some logic during assignment statements that you can either leave with default values by using auto-properties, as in the property named AutoProperty, or can have custom logic defined for their getters and setters, as in the example named CustomProperty.

One important difference to note: since interfaces can only include methods, interfaces cannot expose Fields. They can, however, expose the getters and setters of Properties.

**Class versus Object:**

![devenv_2016-02-22_21-07-25](images/devenv_2016-02-22_21-07-25.png)

The two small code snippets in this screenshot demonstrate the difference between a Class and an Object. Classes are definitions of a data structure which expose a constructor we can invoke in order to create instances of that data structure. An Object is a single instance of a Class. To put it another way: Objects have a point in your code where they are created, then exist until they are eventually cleaned up by the garbage collector when they are no longer referenced. Classes exist at all times after compilation, and are used to create Object instances.

**Interface versus Implementation versus Inheritance**

![devenv_2016-02-22_21-14-44](images/devenv_2016-02-22_21-14-44.png)

Here we see examples of Inheritance, an Interface, and the Interface’s Implementation. An Interface is simply a definition of a collection of methods made publicly available by any class that Implements the Interface. Our Interface declares a single public method named Subtract which takes two integer arguments. But you will notice that IInterface does not define any method body for this method. The method body must instead be defined by any class that chooses to Implement that interface.

If we look at our class named Implementation, we can see that it Inherits from our class named ParentClass, and Implements our Interface named IInterface. The method body of the Subtract method defined in IInterface is actually declared within our Implementation class. If we did not declare public methods that matched all the methods defined in the Interface that our class Implements, this would result in a compiler error.

Notice also that Implementation does does not define a method body for Add. That is instead done in our class named ParentClass. Parent class both **defines**and **implements** the Add method. As a result, our Implementation class will Inherit this method definition from its ancestor class. If we were to invoke the Add method on an instance of Implementation, the code which would execute at runtime would actually be the code declared inside the method body of ParentClass.

Note also that in C# (and any language which does not support multiple Inheritance) – a class can only Inherit from a single class. Conversely, a single class can Implement as many Interfaces as you wish.

**Operator versus Operand**

![devenv_2016-02-22_21-27-28](images/devenv_2016-02-22_21-27-28.png)

Operators are symbols (or collections of symbols) in code which perform some operation on the values immediately adjacent to them. The values which are operated on in this way are called Operands. C# has Operators which take one, two, or three Operands. They are called Unary Operators, Binary Operators, and Ternary Operators, respectively.

In the screenshot above, I have highlighted each Operator in green, and each Operand in red. (Note: the equals sign ‘=’ is the assignment Operator, but I did not highlight it since it won’t be discussed directly here.)

Beginning at the top, we have the binary Addition Operator ‘+’ which accepts two numerical Operands and returns their sum.

Next we have the unary Logical Not Operator ‘!’ which accepts a single boolean Operand and returns the inverse of its value.

And last we have the Ternary Operator ‘?:’ – to which we are passing the result of a Logical Equality Operator whose Operands are the variable ‘a’ and the integer constant ‘5’. Depending whether this value is true or false, determines whether the Ternary Operator returns its second or third operand respectively. If ‘a’ is equal to 5 when this statement executes, then 0 will be returned, otherwise 1 will be returned.

**Line versus Statement versus Expression**

![devenv_2016-02-22_21-42-29](images/devenv_2016-02-22_21-42-29.png)

An Expression is a sequence of Operands and Operators which evaluates to a single value. In the example above, ‘5 + 4’ and all of the other arithmetic operations we perform are Expressions.

Lines refer to a single line of code, which may contain one or more Statements and Expressions.

Statements refer to many actions your program might execute. As you step through your code using a debugger, you will sometimes find that individual Lines of Code may be hit multiple times by the debugger. This is because the C# Debugger breaks on individual Statements, rather than individual Lines.

In our example above, the first two lines each contain a single Statement: an integer variable declaration statement, and an assignment statement which stores the result of the Expression 5 + 4 into that variable.

The third line, however, contains 3 variable declaration Statements, 3 assignment Statements, and 3 arithmetic expressions.

**Functions versus Methods**

For this example I will use Javascript, since C# does not have a way to define Functions which are not also Methods:

![devenv_2016-02-22_21-55-33](images/devenv_2016-02-22_21-55-33.png)

Functions are definitions of a collection of Statements which may be executed at runtime.

Methods are specific examples of Functions whose context for execution is an instance of an object. This means that those methods will have access to a particular object’s private data, which may not otherwise be accessible. Most languages including Javascript and C# use the ‘this’ keyword to as a reference to the object instance to which a Method belongs at runtime.

In our example above, Add would commonly be described as a Function, while Subtract could be considered a Method, since it depends on being executed within the context of a particular object, whose properties it will access with the ‘this’ keyword.

**Parameters versus Arguments**

![devenv_2016-02-22_22-02-16](images/devenv_2016-02-22_22-02-16.png)

Parameters and Arguments are closely related and often confused (in fact I only just recently learned the difference thanks to [this StackOverflow post](http://stackoverflow.com/a/1663724/1504529 "Thanks, Stack Overflow!"))

Parameters are the names in a method declaration which refer to values which can be passed to a method at runtime when it is invoked.

Arguments are the values passed in to fulfill a method’s Parameter values when it is actually invoked. I have indicated the Arguments in the screenshot above in red, while the Parameters are indicated with green.

 

* * *

Hopefully, this blog will have helped you learn to better distinguish between some common programming terms, as well as identify the specific code artifacts to which they refer.

If you found this useful, let me know in the comments and I may do another blog about programming terminology. Let me know what terms you feel the least comfortable with or see other programmers confuse most often and I’ll discuss them in a future blog post!
