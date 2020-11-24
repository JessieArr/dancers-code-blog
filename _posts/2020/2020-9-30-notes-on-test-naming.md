---
title: Notes on Test Naming
author: Shawn
date: 2020-09-30 12:00:00 -0600
categories: [Testing]
tags: [Testing, Naming]
---

> There are only two hard problems in programming: cache invalidation, naming things, and off-by-one errors.

One of the tricky things about talking and writing about the various types of automated tests is simply naming them. Terms like “Unit” and “Integration” test are heavily overloaded, and the distinction between categories of test is not always trivial to draw.

In fact for many developers with minimal exposure to test automation they may use the term “unit test” to refer to all forms of coded test. Further it is common for “System” and “Integration” tests to be used interchangeably by various organizations to refer to collections of software working together along with data. 

## What's Important

Ultimately the names used for various test types are not that important, but it is important to have a standardized terminology within your development team so that a particular name carries a consistent meaning when used by anyone on the team.

Beyond names, there are 4 general functional aspects of tests which do matter, which correlate loosely to the names we give to tests:

- **Test Scope:** The amount of code exercised within the scope of executing a test.
- **Test Technique:** The method by which the test asserts something about our codebase. Some functionality we wish to test may require a certain technique and be impossible with others.
- **Test Duration:** How long it takes to execute the test.
- **External Dependencies:** Whether the successful execution of the test depends on something outside of our codebase, such as an API, data in a database, or something installed on the local machine.

These 4 factors carry important semantic meaning for our tests in terms of when and why we would execute them, and therefore having consistent names for tests which vary according to these factors is critical to being successful in implementing an automated testing strategy.

With that in mind, below I will define 4 categories of test that will be used in this blog series to broadly describe tests according to *test scope* and **external dependencies.**

**Unit Test:** The smallest scope of test: tests a single class or method in the simplest way possible that still exercises meaningful logic. No external dependencies outside of our code.

**Integration Test:** A larger scope of test, which exercises one or more class in conjunction. This includes tests which may exercise nearly our entire codebase, but *without* taking on any external dependencies outside our codebase.

**System Test:** Testing our codebase in a live configuration, alongside any external dependencies such as APIs, databses, etc. that it may depend on.

**UI Test:** Exercising our codebase through interacting with the actual UI that the user might see. This could be done through Selenium (web apps) Appium (mobile apps) or native testing frameworks for desktop apps, along with any dependencies it may have.