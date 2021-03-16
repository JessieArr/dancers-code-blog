---
title: System Testing
author: Shawn
date: "2021-03-15"
categories: [Testing]
tags: [System Tests]
---

For the purposes of discussion in this blog, the term System Tests will refer to tests in which multiple codebases are working together (see [Notes on Test Naming]({% post_url 2020-09-30-notes-on-test-naming %}) for more details).

In a System Test, we will test classes from our codebase along with upstream or downstream dependencies of our code, in order to determine that interactions within our entire software system work as we expect.

Below is a diagram of two different System Test scopes:

![System Test Diagram](/content/2021/03/system-test-diagram.png)

You can see that the scope of System Tests is always somewhat flexible, but it will begin in our codebase and the flow of code execution will eventually leave our application code during an invocation of an API call and enter some dependency that exists outside of our codebase.

This may be an API, a file on the local filesystem, or anything else that isn't directly controlled by our application.

## Minimal Use of Mocks

While Unit and Integration Tests heavily mock dependencies so that we can make assertions about our code's behavior in isolation, these types of tests allow us to determine what will occur when our code operates with data and systems outside our codebase. There are a number of failure modes that will often only be detected when interacting with live data from other systems, such as issues caused by latency, intermittent failures in downstream dependencies, serialization/deserialization errors, and invalid assumptions about the type of data we can expect to get back from other systems.

By using System Tests, we can ensure that our code will actually work when it comes time for it to be put into a real environment with other running codebases. They also provide a useful way of testing what happens if we send invalid requests to downstream systems, and that our code properly handles these failure scenarios with exception handling, logs, etc.

## External Dependencies

Due to the nature of System Tests, we are no longer operating entirely within our application's memory space like we have been for Unit and Integration tests. As a result, these tests will perform more slowly due to things like network latency and disk I/O speeds. As such, we should maintain a relatively small number of System Tests, and test as much of our application's behavior in Integration and Unit tests as possible.

These tests are also subject to possibly failing due to issues outside of our application. For instance, imagine that we are running a System Test that interacts with a database, and the database is down for maintenance. Or that an experimental branch of a downstream API has been deployed into our test environment which contains a bug. In situations like this, our System Tests may fail for reasons outside of our codebase!

## Build Validation

This is an important consideration when running tests as part of your build process. As a general principle, I recommend running only Unit and Integration tests to validate builds of your codebase, and instead using tests like System Tests and UI tests which have a scope that extends outside of your codebase to test deployments to a particular environment. In this way, we are validating not just our application, but the entire environment that our application runs in.

In the context of a [CI/CD Pipeline]({% post_url 2019-11-14-role-of-test-automation-in-a-ci-cd-pipeline %}), we should view System Tests as a type of In Situ Test - that is, a test that verifies not only our application's behavior, but validates (or invalidates) the environment as well.