
As said before, the `TestCaseResult` object provides some methods to set some expectations on the result.

Depending on the type of the expected result value, different methods are available.

- If the expected result is an `Ok` value, you can use the `shouldBe`, `shouldHave` or `shouldMatch` methods.
- Otherwise, you can use the `shouldFail` method.

All these methods take a single argument of type `Expectation` and return an `ExpectationChain` object.


### **Expectation object**

`Expectation` object is a sealed class that represents the expectation to set on the result of the test case.

In another word, it is the condition that the result must satisfy to pass the test.

Expectation class has two implementations:
 
- `Expectation.OnFailure` : to set an expectation on an `Err` value.
- `Expectation.OnValue` : to set an expectation on an `Ok` value.

### **ExpectationChain object**

`ExpectationChain` object allow you to chain multiple expectations on the result of the test case.

It exposes a single method `and` that takes an `Expectation` object and returns a new `ExpectationChain` object.

### **Expectations on an `Ok` value**

On an `Ok` value, you can set three types of expectations:

- **`shouldBe`**

    with the following implementations:

    - `Null` : to check if the result is `null`.
    - `NotNull` : to check if the result is not `null`.
    - `EqualTo` : to check if the result is equal to a given value.
    - `NotEqualTo` : to check if the result is not equal to a given value.
    - `Between` : to check if the result is between two values. ⚠️ The result must be `comparable`.
    - `GreaterThan` : to check if the result is greater than a given value. ⚠️ The result must be `comparable`.
    - `LessThan` : to check if the result is less than a given value. ⚠️ The result must be `comparable`.


=== "Java"
    ````java
      @Test("Parse '123' to integer should give 123")
      void testParse(TestCase<String, Integer> testCase) {
          testCase
              .given("a string '123'", "123")
              .when("parsing it to integer ", Integer::parseInt)
              .then("the result should be 123", result -> 
                  result.shouldBe(notNull()).and(equalTo(123))
              );
      }
    ````
=== "Kotlin"
    ````kotlin  
        @Test("Parse '123' to integer should give 123")
        fun testParse(testCase: TestCase<String, Int>) {
            testCase
                .given("a string '123'") { "123" }
                .`when`("parsing it to int") { it.toInt() }
                .then("the result should be 123") { 
                    it shouldBe notNull() and equalTo(123) 
                }
        }
    ````
- **`shouldHave`**
  
    with the following implementations:

    - `Size` : to check if the result has a given size.
    - `AnItemEqualTo` : to check if the result has an item equal to a given value.

   ⚠️ The result must be a `String`, an `Iterable` or an `Array`. 


=== "Java"
    ````java
      @Test("Add 'a' to ['b', 'c'] should give ['b', 'c', 'a']")
      void testParse(TestCase<List<String>, List<String> testCase) {
          testCase
              .given("a list", List.of("b", "c"))
              .when("'a' is added to the list", list -> {
                  list.add("a");
                  return list;
              })
              .then("the list should contains 'a'", result -> 
                  result.shouldHave(size(3)).and(anItemEqualTo("a"))
              );
      }
    ````
=== "Kotlin"
    ````kotlin  
      @Test("Add 'a' to ['b', 'c'] should give ['b', 'c', 'a']")
      fun testParse(testCase: TestCase<String, Int>) {
          testCase
              .given("a list") { listOf("b", "c") }
              .`when`("'a' is added to the list"") { it.apply { add("a") } }
              .then("the list should contains 'a'") { 
                  it shouldHave size(3) and anItemEqualTo("a) 
              }
      }
    ````

- **`shouldMatch`**

    with the following implementations:

    - `One` : to check if the result matches a given predicate.
    - `All` : to check if the result matches all the items of a given list of predicates.
    - `None` : to check if the result matches none of the items of a given list of predicates.

=== "Java"
    ````java
      @Test("Parse '123' to integer should give 123")
      void testParse(TestCase<String, Integer> testCase) {
          testCase
              .given("a string '123'", "123")
              .when("parsing it to integer ", Integer::parseInt)
              .then("the result should be 123", result -> 
                  result.shouldMatch(all(
                        Map.of(
                            "is not null", s -> s != null,
                            "equal to 123", s -> s == 123
                        )
                  ))
              );
      }
    ````
=== "Kotlin"
    ````kotlin  
        @Test("Parse '123' to integer should give 123")
        fun testParse(testCase: TestCase<String, Int>) {
            testCase
                .given("a string '123'") { "123" }
                .`when`("parsing it to int") { it.toInt() }
                .then("the result should be 123") { 
                    it shouldMatch all(
                        mapOf(
                            "is not null" to { it != null },
                            "equal to 123" to { it == 123 }
                        )
                    ) 
                }
        }
    ````

### **Expectations on an `Err` value**

On an `Err` value, you can set only one type of expectation: `ShouldFail`.

`ShouldFail` expectation has two implementations:

- `WithType` : to check if the error is an instance of a given type.
- `WithMessage` : to check if the error message is equal to a given value.


=== "Java"
    ````java
      @Test("try to divide by zero")
      void testParse(TestCase<Integer, Integer> testCase) {
          testCase
              .given("a number", 3)
              .when("divide it by zero", i -> i/0)
              .then("result should be a failure", result -> 
                  result
                    .shouldFail(withType(ArithmeticException.class))
                    .and(withMessage("/ by zero"))
              );
      }
    ````
=== "Kotlin"
    ````kotlin  
        @Test("try to divide by zero")
        fun testParse(testCase: TestCase<Int, Int>) {
            testCase
                .given("a snumber") { 3 }
                .`when`("divide it by zero") { it/0 }
                .then("the result should be a failure") { 
                    it shouldFail withType(ArithmeticException::class) and withMessage("/ by zero")
                }
        }
    ````