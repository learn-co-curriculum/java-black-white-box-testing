# Black or White Box Testing

## Learning Goals

- Explain black/white box testing.

## Introduction

As the size and complexity of the software systems we build increases, it's
important to scale the type of testing that is being done with the system with
its complexity.

Unit testing is technical testing by definition in that it concerns itself with
the implementation details of the functionality it's testing. This is very
useful and plays a crucial role in building reliable and maintainable systems.
There are two important limitations with this type of testing, however:

1. Because it's "technical testing", the range of people who can write these
   tests is restricted to people familiar with the implementation details of the
   components being tested. This means we might test that we built the component
   properly, but we are at risk of not testing that we built the right
   component.
2. Unit testing is focused on the workings of a single component. As the system
   grows, these single components interact with each other and the way they
   integrate with each other can be a great source of bugs.

## White Box Testing

**White box testing** is a type of testing that is performed with knowledge of
the inner workings of the software. This means, the tester needs to know the
design, implementation, and structure of the software.

Unit testing is a prime example of white box testing, where we care about the
underlying implementation details of what we're testing.

White box testing techniques are based on code coverage, 
which measures how much source code is executed by the tests.
While there are many code coverage techniques, some basic techniques include:

- **Function coverage:** The tests cause each function (method) to be executed at least once.
- **Statement Coverage:** The tests cause all executable statements in a program to be executed at least once.
- **Branch Coverage:** The tests cause all branches of all control structures in a program to be executed at least once.
  - For example, the conditional statement `if (x  < 5)` requires at least 2 tests (`x < 5` is true, `x < 5` is false).
- **Condition/Predicate Coverage:** The tests cause each boolean sub-expression in a compound boolean expression
  to evaluate to `true` and `false` at least once.
  - For example, the expression `(isRaining || isSnowing)` requires a minimum of 4 tests that evaluate as shown:
    - `(true || true)`
    - `(true || false)`
    - `(false || true)`
    - `(false || false)`


## Black Box Testing

**Black box testing** is a type of testing that is performed without any
knowledge of the inner workings of the software. This means that black box
testing can be performed by those who are not necessarily developing the
software or writing any of its code. Examples of black box testing include:

- **Functional testing**: testing specific functional aspects of a system,
  regardless of how many underlying components are involved in implementing that
  functionality. Some examples of functional test could be:
    - Checking to make sure the functionality and features on a website is working
      correctly. This could include looking at the menus, images, and links.
    - Regression testing is usually thought to be a subset of functional testing
      in that it double-checks that everything is working properly after a
      change has been made.
- **Non-functional testing**: testing the "non-functional" aspects of a system.
  This type of testing looks more at the quality of the system rather than if
  its features work as expected. Some examples of non-functional testing include:
    - Performance testing to ensure the system can perform in a responsive and
      timely manner despite several concurrent user requests.
    - Security testing to test how secure the system is in terms of protecting
      itself from malicious attacks.

Non-functional testing, such as performance and security testing, is out of
scope for this section, so let's focus on functional testing.

It may seem like there would be a lot of overlap between "functional testing"
and "unit testing", but the difference between the two is profound:

- Unit testing focuses on making sure the code works as the developer intended
  it to work.
- Functional testing focuses on making sure the software works as the users need
  it to work.

In other words, one focuses on "building the thing right" while the other
focuses on "building the right thing".

This is a profound distinction because it does not matter if the code runs
perfectly every time if it does not actually solve the problems that its users
need solved.

Let's consider a simplified version of a real-life example. Your team has been
asked to build a "bill splitter" calculator:

- There will be a number of participants.
- There will be a total for the bill.
- You've been asked to write the method that performs the division.
- You've been told you will always be dealing with integers for all parameters
  and for the return value.
- You have not been given the "bill split" context, so you don't know how this
  "divide" method will be used.

Here is some sample code you might have written:

```java
public static int divide(int amountToSplit, int numPeople) {
    return amountToSplit / numPeople;
}
```

Here is the unit testing code you might have written as well:

```java
@Test
void divideEven() {
    int split = SplitCalculator.divide(100, 4);
    assertEquals(25, split);
}

@Test
void divideOdd() {
    int split = SplitCalculator.divide(100, 3);
    assertEquals(33, split);
}
```

You were careful to test both cases where the result of the division is whole
and where the result is not whole. In doing so, you assumed the default Java
behavior of rounding _down_ when diving two integer numbers and getting a
decimal number back is the proper behavior.

In other words, your unit tests properly validate that the code works in the way
that you, the developer, intended it to work.

It's not until the business gets the entire "split calculator" app that they
realize that decimal numbers are being rounded down and that their customers in
their restaurants consistently come up short when trying to pay their bill based
on what the calculator tells them. This is a good example where black box
testing could have been useful on top of the unit testing.