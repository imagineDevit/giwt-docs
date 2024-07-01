---
title: Introduction
---

**Giwt** is a <span class="text-blue">_Java_</span> _testing_ framework based on **_JUnit platform_**.

A <span class="text-blue">_Kotlin_</span> version (**Giwt-kt**) is also available.

In this documentation, we will use the term **Giwt** to refer to both versions.
But examples will be provided for both languages.


**Giwt** allows developers to write tests in a more readable and understandable way using the `given-when-then` style.

Some libraries such as _JGiven_ or _Spock_ already offer the possibility of writing tests in this _style_.
But depending on the sensitivity of the developer, setting up tests with these libraries can be a little complex.

**Giwt**, by implementing its own _test engine_, is committed to reducing this complexity.


### **Example**

Here is a simple example of a test written in `Giwt`:

=== "Java"
    ````java
    @Test("Parse '123' to integer should give 123")
    void testParse(TestCase<String, Integer> testCase) {
        testCase
            .given("a string '123'", "123")
            .when("parsing it to integer ", Integer::parseInt)
            .then("the result should be 123", result -> result.shouldBe(equalTo(123)));
    }
    ````
=== "Kotlin"
    ````kotlin  
    @Test("Parse '123' to integer should give 123")
    fun testParse(testCase: TestCase<String, Int>) {
        testCase
            .given("a string '123'") { "123" }
            .`when`("parsing it to int") { it.toInt() }
            .then("the result should be 123") { it shouldBe equalTo(123)}
    }
    ````

_Note that the test method takes a `TestCase` parameter. It is the fundamental concept of **Giwt**. We'll talk about this in more detail later._

### **Installation**


=== "Java"
    [![Maven Central](https://img.shields.io/maven-central/v/io.github.imagineDevit/giwt)](https://central.sonatype.com/artifact/io.github.imagineDevit/giwt/overview)

    Add the following dependency to your `pom.xml` file:

    ````xml
    <dependency>
        <groupId>io.github.imagineDevit</groupId>
        <artifactId>giwt</artifactId>
        <version>${version}</version>
        <scope>test</scope>
    </dependency>
    ````
=== "Kotlin"
    [![Maven Central](https://img.shields.io/maven-central/v/io.github.imagineDevit/giwt-kt)](https://central.sonatype.com/artifact/io.github.imagineDevit/giwt-kt/overview)

    Add the following dependency to your `pom.xml` file:
    ````xml
    <dependency>
        <groupId>io.github.imagineDevit</groupId>
        <artifactId>giwt-kt</artifactId>
        <version>${version}</version>
        <scope>test</scope>
    </dependency>
    ````
    or if you are using `Gradle` add the following dependency to your `build.gradle` file:
    ````kotlin
    testImplementation("io.github.imagineDevit:giwt-kt:${version}")
    ````





