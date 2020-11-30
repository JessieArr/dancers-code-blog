---
title: "Legacy Code Explained for Non-Programmers"
author: Shawn
date: "2018-07-25"
categories: [Programming]
tags: [Tech Debt]
---

> You do not truly understand something unless you can explain it to your grandmother.
> 
> – Albert Einstein

I often get asked by non-programmers what legacy code is. I’ve heard many programmers try to answer this question over the years, and have yet to hear a good explanation that a layperson could be easily expected to grasp (and haven’t yet delivered one myself, either.)

However I think Einstein was right when he said the quote above. In order to truly understand anything, regardless how complex it is, you need to be able to draw parallels between a complex system and something simpler and easier to picture in your mind.

In software development, we call this an abstraction. It’s essentially the way you understand what a car is. Cars are extremely complex, with thousands of parts and many makes and models. But because we have a simple and broad understanding of _what a car is,_ anyone can quickly identify whether something is a car or not, all without needing to pop the hood and understand its inner workings.

So in order to further solidify my own understanding of how maintaining code, especially the dreaded **legacy code** works – I have set myself the task of explaining it in the simplest terms I can.

Legacy code is basically old code that is no longer well understood (and indeed, may never have been.) Yet such code often runs many of the oldest and most important software systems in the world. The more important code is, the less likely we are to change it, and the easier it is to let things stay in a bad state simply because they’re _working._ 

You probably don’t want your bank to change the code that keeps track of how much money you have unless there’s a dire need. If it ain’t broke – don’t fix it.

I think the best analogy I can give for being asked to maintain a code base is that it is like being asked to edit a novel series. (Choose your favorite here, Game of Thrones, Harry Potter, etc.)

There are enough books that you cannot easily read them all every time you have to make a change, so you’ll often rely on your memory of the last time you read it. Some changes may seem fairly straightforward: rename a character. Let’s say you want to change Eddard Stark’s name to William Stark. This sounds simple enough, simply use a text editor to find and replace Eddard with William.

This works great, but what if there were two characters named Eddard? Now we have a problem. We’ll need to find each place the name Eddard is used, then read the paragraph around it and understand it so we know which character’s name we’re changing. And if we make a mistake, calling one character by another’s name can be very confusing for the reader.

So we can see that even the simplest of changes may require us to have at least a basic understanding of the book near where we make changes. But that can’t be _too_ error prone, so where do bugs come from?

Well let’s assume we want to make a change that’s more complex: let’s say we want to rewrite the series so that the winners of a battle are instead the losers. This can have serious implications for the characters and groups in the book, and we can’t just search for a character’s name to find all the places affected – this will require plot changes.

So we’ll need to understand what areas of each book are ones that would be affected by the outcome of that battle. Future battles may never have happened, different characters may have died or survived. This will have an impact on how we want the plot to go in many future chapters.

This is a pretty big task. If we are intimately familiar with the books, we can speed the process up, but if the book series is large or if we’re new at our job and haven’t read them all, this may necessitate a whole lot of reading simply so we know what changes to make. Many chapters may have to be read just so we know how to rewrite a single paragraph. In a large series, we may have so many changes to make that we have two people working on it – they may even accidentally contradict one another.

So this is all pretty standard practice for authors, they work slowly and deliberately, and have editors to help them, and manage to get books together without too many glaring errors (at least after all the grammatical and plot errors are found, and the editing and rewrites are done. In the software world those are called ‘bugs.’)

Why can’t software developers just do the same thing?

This is where **Legacy Code** comes in: let’s assume the plot weren’t so straightforward. Let’s say our book is about time travel, and the actions of one character in the past could have many implications for many characters in many places at any point in the future.

If a character overthrows an evil government 100 years in the past, we may be looking at a complete rewrite of the rest of the book series, or at least a complete read through of the whole series to be sure we haven’t missed anything.

There’s no longer any convenient ways for us to know what characters and events may be affected by this plot change we’ve made, so the list of things that may have to be checked and changed is essentially “everything.”

But let’s say our publisher wants our book series published by 5pm on Friday (or you and thousands of other users have told the company that publishes the software in question that you **really** want that bug fixed right away, in no uncertain terms.)

Then maybe we don’t take the time to reread the whole series. Maybe we talk to the guy who knows it best and ask him for a list of every place that may need to be rewritten. After a few hours he comes back to us with the most exhaustive list he can come up with on short notice and says “I think that’s everything.”

A few days later, we’ve rewritten our books, changed everything the guy who knows the series best told us to, and we make our 5pm on Friday deadline. We got everything.

We’re pretty sure we got everything.

We’re kinda sure….

And this, ladies and gentlemen non-programmers, is where bugs come from. This is how legacy code causes them. So how do we make it better? How can we have **good code** instead of icky **legacy code**?

Let’s say that instead of our book series, we instead had an anthology of short stories. The stories may share characters, take place in the same world, and occur at some of the same locations.

Because each story is meant to stand alone, there’s only a limited number of ways one story can affect another. Because each story has its own plotline and a small list of characters and locations, it’s easy for one of our editors to remember which are involved in each story.

We could even draw a diagram of which characters and locations are shared between which stories, allowing us to change one story and know immediately how our changes will affect others.

We may even give each story a handy name to help us remember what goes on in it, such as “Critical Bank Account Balance Code.”

So now we’re in a much better spot if we want to make changes. A quick read-through of a single short story will let us know what characters and locations are involved. The title will give us hints to tell us about a story we haven’t read or jog our memory about one that we read several months ago. We can even consult our not-too-complex diagram about the relationships between the stories to understand what impacts a change may have on our series as a whole.

So that’s it then. That’s what programmers are talking about when they use phrases like “legacy code”, “good code”, and where a lot of bugs come from. Basically programmers complaining about legacy code are complaining that the last writer left them a huge novel series with a convoluted plot to edit, and they’re wishing that instead they had a nice series of self-contained short stories to work with.

When they say they want to “refactor” code, they want to take a novel (or a big chunk of code) and turn it into a series of short stories that will be easier to work with and discover errors and plot holes in.

So bear this in mind from now on when you hear your programmer friends throwing around jargon and lamenting things like ‘NullReferenceExceptions’ – we’re just trying to make sure we can keep writing a story that ends with you using some software happily and then going to do something more important, rather than a bad ending where you’re screaming at your computer or a hacker gets your data.
