---
title: "SOLID By Example"
author: Shawn
date: "2018-07-25"
categories: [Programming]
tags: [Clean Code]
---

So I’ve recently been discussing SOLID principles with some engineers who are unfamiliar with them, and have realized that a good set of practical examples would be really useful for programmers who haven’t had professional experience with SOLID come to understand it. I won’t claim to be an expert at SOLID, so this is mostly an exercise for myself and a resource geared towards those who are less familiar with the SOLID principles and how to put them into practice when architecting applications in a modern object-oriented language.

To this end, I will take a very simple WPF application which uses a REST client to pull data from an online REST API. Then I will apply SOLID principles in a refactor to make its structure more testable, extensible, reusable, and maintainable. The [example repository can be found on Github](https://github.com/JessieArr/SolidByExample "Solid By Example Github") and is written in C#, but the basic principles apply to all object-oriented languages.

In the coming weeks I will create 5 more blog posts, each centering around one of the SOLID principles:

- Single Responsibility Principle
- Open Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

I hope that newer developers will be able to learn from this, and that those of you who are already familiar with SOLID principles will find it to be a useful example!
