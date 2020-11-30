---
title: "3 Ways to Avoid Being Burned by State"
author: Shawn
date: "2018-07-25"
categories: [Programming]
tags: [Clean Code]
---

If I were to ask you to tell me what the return value of x were after the following lines of C# code executed – could you?

``` c#
var y = 5;
var x = example.Foo(y);

You’d probably ask me to see the implementation of Foo before feeling comfortable guessing the behavior of the method. So let’s take a look at Foo’s contents:

public int Foo(int num){
  return num + this.z;
}
```

Now could you tell me the value of x? Nope, not until runtime, because you don’t know the _state_ of `example.z`. Depending on state, particularly mutable state, is one of the most common ways to build complexity into your code. The result of a single line of code that depends on state could potentially be affected by _every line of code that has executed before it which modifies our program’s state._ This increases our program’s complexity exponentially.

So let’s take a look at 3 simple techniques for avoiding state in our code.

**Write Functions and Methods as Pure Functions.**

Let us contrast the previous implementation of Foo with a new one which will allow us to achieve the same thing:

``` c#
public int Foo(int num1, int num2){
  return num1 + num2;
}
```

And then invoke it like so:

``` c#
var y = 5;
var z = 10;
var x = example.Foo(y, z);
```

Now you can tell me exactly what x will be after Foo executes, at compile time. This is because we no longer depend on the internal state of the object `example`. We have created a [pure function](http://en.wikipedia.org/wiki/Pure_function), which is one of the most powerful ways of avoiding being burned by state. Pure functions have two properties:

1. The function always returns the same result when invoked with the same arguments.
2. The function has no side effects. None of our program’s internal state is modified by invoking the function. (until we store its return value.)

Because they are explicit about the state they depend on (the function’s arguments) and because they do not mutate any of the program’s state, they reduce the complexity of our code tremendously.

We can compose an arbitrarily complex series of calls into pure functions, and if we know the state of the inputs to those functions, we can prove what the output will be with 100% accuracy. This is the great power of functional languages, however it is important to note that one can program in a functional way and reap the benefits of pure functions in nearly any modern language.

Sometimes however, we need state. After all, sometimes we want to store data somewhere and retrieve it later. Databases, File I/O, DTOs, and Caching are all great examples of this. We can’t get away from state entirely and still be able to do anything useful.

So let us look at another way we can avoid being burned by state:

**Make Stateful Data Structures Immutable**

We can relax the first property of a pure function when needed (depending on outside state), while still enforcing the second property (not mutating data). With this in mind, let’s take a look at one possible implementation of our example object’s constructor:

``` c#
public class Example
{
  public int z;
  public Example(int zValue)
  {
    z = zValue;
  }
  public int Foo(int input)
  {
    return input + this.z;
  }
  // Other object methods here
}
```

Now let’s use this new implementation of Example to accomplish the same task we did before:

``` c#
var example = new Example(10);
example.ModifyZ();
var y = 5;
var x = example.Foo(y);
```

By looking at this code, can you be certain the value of x without running it? It’s true that we could inspect the ModifyZ method to see whether and how it mutates Example.z – but there is a better option. What if we made z immutable? Then we could be certain that z would _always_ have the value assigned during the constructor of Example:

``` c#
public class Example
{
  public readonly int z;
  public Example(int zValue)
  {
    z = zValue;
  }
```

Now let’s take another look at the same code snippet above:

``` c#
var example = new Example(10);
example.ModifyZ();
var y = 5;
var x = example.Foo(y);
```

This time, because we know that z is immutable, we can be certain without executing this code that x will be 15 after these lines execute. The behavior of the ModifyZ method no longer has the ability to affect the state we depend on because z is immutable.

But what can we do if we can’t make some of our state immutable? A database, cache, or file system are all designed to be modified and accessed from many different locations in code.

**Make Dependency on Mutable State Explicit.**

In the last section, we looked at what would happen if we relaxed the first property of mutable functions while still enforcing the second. Now let’s look at how we can benefit from relaxing the second property while still enforcing the first. Let us assume that our Example class contains a DTO parameter which is an arbitrary struct. Below is a possible implementation of the Bar method on our Example object:

``` c#
public void Bar(int input)
{
  this.fileStream.WriteLine(input + this.DTO.z);
}
```

We write a single line to the file, containing the sum of the function’s input and the z parameter of the Example object’s DTO. Now let’s use this new Bar method:

``` c#
var example = new Example(10);
example.ModifyDTO();
var y = 5;
example.Bar(y);
```

Looking at this code, we have no way to be sure what will be written to the file without examining the contents of the ModifyDTO method. But let’s look at another way we might implement the Bar method to achieve the same thing:

``` c#
public void Bar(int num1, DTO data)
{
  this.fileStream.WriteLine(num1 + data.z);
}
```

And let us assume that the implementation of our DTO struct was as follows:

``` c#
public struct DTO
{
  public int z;
}
```

And the following sample code:

``` c#
var example = new Example();
DTO data;
data.z = 10;
var y = 5;
example.Bar(y, data);
```

Now we can be certain what will be written to the file because we can easily follow the DTO struct throughout its entire lifetime within our function. Even though its state is mutable, we can limit the code which might modify its state to code which has a reference to it.

By using functions that have no external dependencies outside of the function arguments, we make our dependencies explicit at the time the function is invoked, which makes debugging much easier. And by ensuring that objects like the above DTO which have mutable state do not give out persistent references to themselves, we can drastically reduce the scope of code capable of modifying them.

A good way of identifying candidates for these sorts of changes are methods that either have a void return value, or accept no arguments. Methods with no return value have no reason to be invoked _except_ for their side effects. Methods with no arguments either do something extremely trivial, or depend internally on state in order to accomplish something useful. Every time you find yourself writing a void function, or a function with no arguments, consider whether it might be better implemented in a less stateful way.

The more we reduce our dependence on state, the more we untangle the complexity in our code. Often times widespread dependence on mutable state introduces a lot of complexity and uncertainty into code which could easily be rewritten to avoid most or all of its state. Avoiding state where possible, and using it in deliberate and careful ways when it is needed, are excellent ways to write much more maintainable code!
