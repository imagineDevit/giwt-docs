---
title : Test Case
---
**TestCase** is the fundamental concept of **Giwt**. 
<br> _It allows developers to precisely describe the test case while implementing it_.

!!! info "State of play"
    In development, when we write a test, we test the result of executing a function.
    <br>And a function is a piece of code that takes an input and returns an output.

The **Giwt** _TestCase_ object was designed based on this principle :
it is represented as a generic class that takes two type parameters **`T`** & **`R`** :

----
!!! note "T : the state" 
    `T` is conceptually considered as the type of the test case _state_.

In other words, the type `T` is the type of the method to test parameter(s).  

But a method can have no, one or multiple parameters, so **Giwt** give you a way to represent them.

- When the method to test takes _**no parameter**_, use **`Void`** (for Java) or **`Unit`** (for Kotlin).
- When the method to test takes _**one parameter**_, use the type of this parameter.
- When the method to test takes _**multiple parameters**_, use one of [**_Args_**](https://javadoc.io/doc/io.github.imagineDevit/giwt-core/latest/io/github/imagineDevit/giwt/core/Args.html, " Args object is provided by giwt to wrap the list of method parameters.") object implementation corresponding to the method signature.
    
!!! info "Args"
    The `Args` _interface_ is provided by **Giwt** to wrap the list of method parameters.
    <br>It has generic implementations that takes from 2 (`Args.Args2`) to 10 (`Args.Args10`) type parameters.
    <br>For example, if the method signature is `void method(String s, int i)`, you can use `Args2<String, Integer>`.
----
!!! note "R : the result"
    `R` is conceptually considered as the type of the test case _result_.

Since the testCase execution corresponds to the execution of the method to test, `R` is the return type of this method.

ℹ️ Use **`Void`** (for Java) or **`Unit`** (for Kotlin) if the method to test returns nothing.

After the method to test is executed, the result is wrapped in a **`TestCaseResult<R>`** object. 

!!! info "TestCaseResult"
    As the test can succeed or fail, the `TestCaseResult<R>` object also wraps the result into a sealed class **`ResultValue<R>`** that can be either **`Ok<R>`** or **`Err<R>`** in case of success or failure respectively.
    <br> `TestCaseResult` object provides some methods to set some [expectations](./expectations.md) on the result.

