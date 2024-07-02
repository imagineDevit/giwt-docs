
Writing a test with **Giwt** means clearly stating the different stages of the test using the _**given**_, _**when**_ and **_then_** statements.

Giwt provides three types of statements to describe the test case:

 - [**GivenStmt**](./statements.md/#given-statement) : to describe and supply the input data of the test.
  - [**WhenStmt**](./statements.md/#when-statement) : to describe and run the method to test.
  - [**ThenStmt**](./statements.md/#then-statement) : to describe and execute assertions on the output data of the test.

----
### **Given statement**
    
The **given statement** is represented by the `GivenStmt` class.

It is used to describe and supply the input data of the test and to set up the test environment (mocks, stubs, etc.).

**GivenStmt** can be created from a `TestCase` instance using the `given` method.

It exposes two methods :

   - **`and`** : to add one more given statement to the test case. It is useful to set up mocks or stubs.
   - **`when`** : to create the `WhenStmt` instance associated with the test case.

----
### **When statement**

The **when statement** is represented by the `WhenStmt` class.

It is used to describe and execute the method to test.

**WhenStmt** can be created from a `GivenStmt` instance or directly from a `TestCase` instance using the `when` method.

It exposes a single method `then` that creates the `ThenStmt` instance associated with the test case.

----
### **Then statement**

The **then statement** is represented by the `ThenStmt` class.

It is used to describe and execute expectations on the output data of the test.

**ThenStmt** can be created from a `WhenStmt` instance using the `then` method.

It exposes a single method `and` that add one more then statement to the test case.