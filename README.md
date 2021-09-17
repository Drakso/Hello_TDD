# Testing Software with Unit Tests 🍉

## Testing and Quality Assurance 🔹

In this modern age where we rely on technology for almost everything. This is done through vast numbers of software solutions that are built by programmers. But due to the scale and complexity of today's software, developers often make mistakes, miss edge cases, and interpret the requirements differently than expected. This can lead to disruptions in our work, our environment, and even in our day-to-day life. This is the main reason why software testing and quality assurance got popular, creating an extra layer of revision of a product before it is shipped. Currently, there are many ways to test software and many roles that are involved in executing, documenting, and even building tests.

### Ways we can do testing

* Manual Testing
  * A Manual Tester acts as a User
  * Testing is done manually, by doing the actions expected of a user
  * Specification is consulted on behavior
  * Reports are written to document behavior
  * Bugs are created to document and communicate issues
* Automated Testing
  * Frameworks and Scripts are used to test behavior
  * QA Engineer writes scripts for automated testing in some automated testing frameworks
  * Scripts can then be repeatedly used for testing the software
  * Scripts can also be integrated with a release process
* System Testing
  * Testing is done to a whole system, including all components together
  * It consists of series tests that verify all components work as expected together
  * It includes even external components
  * The testing team does system testing
  * Usually is done at the late phases of a development cycle
* Integration Testing
  * Testing is done to a few components
  * It consists of checking if the targeted components communicate and work as expected
  * Can be done by a Developer or DevOps that writes the integration tests ( Sometimes also done by a professional Testing Team )
  * Integration tests can be done in any environment that can execute and reliably get results from the groups of components
  * Integration testing is done before System testing and after Unit testing
* Unit Testing
  * Smallest testable unit
  * Usually written by developers while they are developing the software
  * Tests are written in a separate project
  * Each test represents one action that does one thing and expect one result

## Unit tests in ASP.NET Core applications 🔹

* When do we write unit tests?
  * We can write unit tests when we finish with the implementation of a method or a class
  * We can also write unit tests before we write our implementation
    * This is called Test-Driven Development
    * We write a bare-bones test that fails -> We write a simple implementation that makes the test succeed -> We refactor the implementation
* Where do we write unit tests?
  * We write unit tests in a special project for Tests
  * There are multiple templates for Test Projects in Visual Studio
  * Most important thing to have for a testing project is:
    * Testing Framework
    * Test Runner
    * .NET Test SDK
* How do we write unit tests?
  * We pick a framework to write unit tests with
  * We create a unit test for every method that does some business logic
  * We create a unit test for every outcome of our methods
  * We create unit tests for positive and negative scenarios
* Structure of a unit test
  * For every class with implementation, there should be a corresponding test class
  * For every method in a class, there should be at least one corresponding test ( usually multiple )
  * Tests can accept arguments and run with different sets of values
  * All tests follow the same structure in the following order:
    * Arrange - We prepare all values that we need for the current test ( expected value, test value )
    * Act - We run the method that we are testing and get the resulting value ( If any )
    * Assert - We write assertions for the expected and resulting values
      * All assertions must be correct for a test to pass
* Conventions and practices
  * The main method we are testing is often named as **sut** ( System Under Test )
  * The result of the method we are testing is often named **actual**
  * Test names should explain
    * What method we are testing
    * What is the behavior we are testing
    * What is the result we expect
  * Examples of test naming conventions
    * MethodName_Scenario_ExpectedBehaviour ( Microsoft Convention )
      * Ex: Sum_TwoIntegerNumbers_ReturnsSumOfIntegers
      * Ex: Divide_IntegerByZero_ThrowsException
    * MethodName_ExpectedBehaviour_Scenario
      * Ex: Sum_ReturnsSumOfIntegers_IfTwoIntegerNumbersProvided
      * Ex: Divide_ThrowsException_IfIntegerDevidedByZero
    * Given_Preconditions_When_Scenario_Then_ExpectedBehaviour ( BDD Convention )
      * Ex: Given_TwoValidIntegerNumbers_When_SumOfIntegerNumbersIsExecuted_Then_CorrectSumIsReturned
      * Ex: Given_OneValidIntegerIsProvided_When_IntegerIsDividedByZero_Then_ExceptionIsThrown

### Unit Test Responsibilities

* Unit tests should be responsible for:
  * Testing one specific piece of software its behaviour ( Method usually )
  * Testing that one specific piece independently from any dependencies
  * Testing the scope of one individual outcome ( If the method has multiple outcomes )
  * Testing the outcome of either positive or negative scenario
  * Being independent of any other tests
  * Executing reliably multiple times
* Unit tests should not be responsible for:
  * External sources of data such as DataBases, Files, APIs
  * External behavior such as mapping, validating, etc.
  * Multiple outcomes at once
  * Multiple scenarios at once
  * Causing side effects to other tests
* All dependencies should be handled separately by:
  * Creating separate tests for all dependencies ( In separate Test Classes )
  * Excluding from tests if tests are not needed
  * Mocking is used to substitute dependencies where they are needed but are not the focus of testing

### Mocking

Mocking is the process of simulating the behavior of real classes and methods that do some business logic, but are not the focus of a test since they are just a dependency. Mocking can be done by writing mock classes and just hardcoding values that we expect to get in our tests. This is very crude but it gets the job done. Another way to do mocking ( used more in general ) is using a mocking framework. Mocking frameworks provide methods for easier creation and configuration of mocks on the spot. We don't have to create special classes to fake the data. We provide the data to the framework, and it creates a mock object or class for us. Some of the more famous mocking frameworks are:

* [Moq](https://github.com/Moq/moq4/wiki/Quickstart)
* [NSubstitute](https://nsubstitute.github.io/help/getting-started/)

### Unit Testing Frameworks

There are many different frameworks for writing and executing unit tests. They are very similar in the way they operate. The difference is the syntax they use and some unique features that add to the experience. The main functionality, structure, and concepts are shared among all of them. Some of the more popular frameworks are:

* [NUnit](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-nunit)
* [xUnit](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-dotnet-test)
* [MSTest](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest)

### Unit tests using NUnit Framework

* Defining a test class
  * A test class is defined by adding an attribute called [TestFixture] above the class
  * In older versions this attribute is required, in newer versions it is not
* Defining a test
  * A test is defined by adding an attribute [Test] above the method
* Defining a setup method
  * Any method with decorated with the attribute [SetUp] is defined as a setup method
  * This method will be executed before every test ( used for setting up dependencies or global fields )

### Project Setup

1. Create an Implementation Project
    * This can be a class library, web application, console application, or any other application where we will have our business logic
2. Create a Test Project
    * Pick the NUnit Test Project
    * In case you don't have the template, create an MSTest project and install the following NuGet packages:
      * NUnit latest
      * NUnit3TestAdapter latest

### Visual Studio Guide

* How to use Test Explorer
  * Click on View -> Click on Test Explorer
  * The test explorer shows up, showing all your tests
  * You can see all tests there, run them and examine results
  * Tests will be grouped by folder, class, and method
  * You can run all at once or one by one
* How to run tests from a test project
  * You can right-click on a test project and click Run Test(s) to run all tests in a test project
  * You can right-click on a test class and click Run Test(s) to run all tests in a class
  * You can right-click on a method and click Run Test(s) to run a single test

### Running Tests in Command Line

* Tests can also be executed independently from Visual Studio, from any command line
* You can run the tests by:
  * Go into your Tests project folder
  * Right-click -> OPen PowerShell window here
  * You can also use the Visual Studio Code command line or any other command line ( make sure to navigate to your project folder )
  * Run the following command
    * dotnet test
  * The command will build the project and execute all tests

## Unit Tests in Action 🔹

## Resources 📚

* [Microsoft Unit Test Best Practices](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
* [Difference between testing frameworks](https://www.lambdatest.com/blog/nunit-vs-xunit-vs-mstest/)
