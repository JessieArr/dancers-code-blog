---
title: "Role of Test Automation in a CI/CD Pipeline"
author: Shawn
date: "2019-11-14"
categories: [Testing]
tags: [Automation]
---

While automated tests can be useful even when their actual execution is triggered manually, even greater benefits can be realized when we also design automation to execute them.

A useful way of thinking about such automated initiation of our tests is in the context of a [Continuous Integration or Continuous Delivery Pipeline](https://smartbear.com/learn/automated-testing/the-continuous-development-pipeline/) (CI/CD.) In this way, as code changes are made and they progress toward being automatically delivered to users, our test automation can ensure that our desired level of quality is enforced via Quality Gates - pass/fail tests that control whether code changes are able to be promoted automatically.

One very common example of a Quality Gate is running Unit and Integration tests as a part of our build. If the tests fail, the build fails and our build artifacts are not made available for deployment into our test environment.

The Pipeline

Let us consider a fairly typical Continuous Delivery Pipeline:

![Click to Enlarge](/content/2019/ci-cd-pipeline.png)

After code is committed, it progresses from left to right. The code will eventually be submitted to a [Pull Request](https://en.wikipedia.org/wiki/Distributed_version_control#Pull_requests) process. The Pull Request process will require an automated build to complete, during which unit and integration tests will be run. If these tests fail, the build will fail, preventing the Pull Request from being completed until code changes are made to allow a passing build. The build process may also include one or more forms of Static Analysis such as [Linting](https://en.wikipedia.org/wiki/Lint_(software)).

Once the build passes, the code changes will be subject to manual review. The manual review process may review the code changes, may deploy the code to a test environment to conduct manual testing and review Non-Functional Requirements, as well as review of UI and UX changes. Once all of the automatic and manual review requirements are satisfied, the Pull Request may be merged.

After being merged, our Continuous Delivery automation should detect a new commit in our mainline branch and will automatically initiate a build. Once this build succeeds, it will be deployed to our mainline test environment. Once there, we may have automated processes which kick off our suite of System Tests and UI Tests. This environment may also be used for other forms of testing such as Chaos Testing, or Load Testing.

Since the code in this environment has already passed both an automatic and a manual review process, it is also a good place for performing manual Exploratory Testing. Exploratory testing refers to manually using software and attempting to identify interesting edge cases in which failures might arise - these edge cases may also be good candidates for automation.

Our Continuous Delivery automation may also automatically promote a successful build from this environment to the next most stable environment (Ex: dev - staging - production.) Depending on your organization and the maturity of your automation, the number of environments may vary, but the principle of Continuous Delivery still holds - when a build is deployed to an environment, we test it against one or more Quality Gates, and if the build passes in this environment, then it is promoted to the next. This process repeats until the code is finally delivered to our production environment and made available to our users.

If our code fails at any point in this process, the development team will be notified. Correspondingly, the later in the process that a defect is detected, the more expensive it can potentially be. Defects that make it into the Pull Request process may waste the time of those reviewing it, as well as time on our build server. Defects that get merged to our mainline branch can disrupt development and testing for other teams working in the same codebase. Defects that make it into our more stable environments can disrupt demonstrations for stakeholders, and of course if a defect makes it all the way to a user it can result in a bad user experience.

The Role of Test Automation

The various types of tests we include in our portfolio make up a series of Quality Gates we use to ensure that code which does not meet our quality standards is blocked from progression until it is improved. This is vital when attempting to successfully adopt a CI/CD deployment style - since our code is deployed automatically, we must create tools that will also ensure its quality automatically.

Following from our Shift Left mindset, we also run our tests as early and often in this process as is feasible. Unit and Integration tests depend only on the code in a given codebase and do not have external dependencies, thus they can be easily run as part of that codebase's build process. System and UI tests depend on the integrity and availability of downstream dependencies such as databases and other APIs, so they are usually run in "In Situ" where our code has access to these other systems.

In short, the goal of a CI/CD Pipeline is to deliver code to users as soon as it is ready, but without test automation and quality gates, we have no automatic way to determine _when_ our code is of a high enough quality to be considered ready.
