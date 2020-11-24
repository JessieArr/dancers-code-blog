---
title: "Goal and Purpose of Test Automation"
date: "2019-11-06"
---

When considering designing a Test Automation strategy, a good first step is to consider exactly what the goal of your test automation will be. It is important to know what test automation can do for you, and what its limitations are.

From the Start

First, let us consider what testing really is: asserting a hypothesis (when I click the "Save" button, data will be written to the database) and then performing a series of actions to test this hypothesis. This applies to all forms of testing, whether manual or automated: the way we test our hypothesis doesn't affect the basic nature of testing.

In the case of software, our hypotheses that we seek to test all have a theme in common: they assert that our software's functionality and non-functional behaviors are "correct."

Yet that last word is itself a common pitfall in test design. If we were to design a physical product and someone used it, and then it began emitting flames - would that be correct behavior? Certainly not if our product is a television, but what about if our product were a gas stove? In the latter case, the inability to get your gas stove to light would actually be a major defect!

Virtually any behavior can be correct depending on what the purpose of our software is. So part of testing is also identifying and documenting the purpose and expected use of the software - an extremely important, but often overlooked task. In many software projects, the automated tests and manual test scripts are the only documentation about the intended behavior of the software that exists.

This is an important fact for two reasons: first, it is important to treat test scripts and automated tests as a form of executable documentation - readability should be prioritized so that they can be used for knowledge sharing in order to improve the long-term maintainability of the project. Second, when formulating your hypotheses, you must realize that a primary problem you face is determining the expected behavior of the software, by communicating with the client, business stakeholders, users, and other team members.

Once the correct functional and non-functional behavior of the software has been identified, it can be thought of as the Quality Statement for the software. If the a particular build or release of the product meets the expectations put forth in the Quality Statement, then it can be said to be of high quality. Conversely, if it fails to meet those criteria, then it will be observed by users and stakeholders to be of low quality and bugs will be reported as a result.

Automating It

The above applies to all testing - both manual and automated. In fact, many software projects depend heavily on manual testing to determine that their behavior is correct. There is no up front investment required to achieve manual testing - one simply needs to use the software to test a hypothesis they have about its behavior.

So why use automated tests at all? It is generally expected that the functionality of software will remain relatively consistent between releases - with the addition of some new features and bug fixes. As a result, the nature of testing is that it is heavily focused around regression testing - that is, ensuring that existing functionality has not been broken by a newer version of the software.

Because regression testing software is a repetitive task, it is a prime candidate for automation. Humans are skilled at creative and exploratory tasks, coming up with novel new approaches to things. Consistency, however, is not our strong suit, and many tasks where a human enters input into a program and checks the output can be performed thousands of times faster by machines than by a human tester.

Thus, we can save a lot of time regression testing our software in the long run if we are willing to take the time up front to create a suite of tests that automate the tasks which would otherwise be carried out by humans (or worse - overlooked by humans due to time constraints!)

Why Not Automate Everything?

If we do automation right, can't we just dispense with manual testers entirely? Getting rid of manual testers or training them all to work as automated test engineers would surely save time and money, right? Nope. Automation is a really important piece of the puzzle in terms of ensuring software quality, but Exploratory (what happens if I click this button while that box is checked...?) and User Acceptance Testing (will the user have a good experience using the software or will they be frustrated or confused?) are vital on any new features.

Earlier we discussed how simply determining the correct behavior of the software is one of the core challenges of testing - this is exactly the hard problem that we should look to manual testers to help us solve. What edge cases did we miss? Does it look nice in all browsers? Is the new feature frustratingly slow when you do certain things? How does it tolerate very long or short input?

As we create new features, the perspective of manual testing is a vital piece in the puzzle to determine not only how the software should behave, but how we can make it better and grapple with edge cases earlier in the software design process. And the information testers gather during these initial rounds of testing should inform the creation of automated tests, which allows us to alleviate our testers of the burden of testing the same things over and over which might otherwise take up the bulk of their time without automation.

Conclusion

Testing is vital to not only ensuring the quality of software, but also determining how the quality should be measured in the first place. Furthermore, automated tests not only give us an easy way to test that our software meets our expected criteria, but it frees more of testers' time to focus on important aspects of testing which can only be done by humans.
