---
title: "My Favorite Programming Blogs"
author: Shawn
date: "2019-03-08"
categories: [Programming]
tags: [Migrated]
---

I maintain a list of programming blogs which have had made a big impression on me, so that I can go back and read them once in a while. I recently realized that there's probably people who would also like to go through them, so... here they are!

### [No Deadlines For You! Software Dev Without Estimates, Specs, or Other Lies](https://web.archive.org/web/20180301043809/http://blog.hut8labs.com/no-deadlines-for-you.html)

This is one of my favorites, because it deals directly with connecting dev work with business value - a gap that is both very important, and very challenging to bridge:

> The core idea is: put uncertainty and risk at the center of a conversation between the developers and the rest of the business (instead of everyone pretending such nasty things don’t exist). Doing so allows the entire business to tackle those genuine challenges _together_.

### [6 Reasons Users Hate Your New Feature](https://www.slicedbreaddesign.com/blog/6-reasons-users-hate-your-new-feature)

> The truth is that users will often ask you for a solution when it would really be more helpful to tell you that they have a problem. \[...\] Sometimes users will tell you that they want a toaster in their car, when what they really mean is that they don’t have time to make breakfast in the morning.

### [Blameless PostMortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/)

> We need to avoid \[the cycle of blame\]. We want the engineer who has made an error give details about why (either explicitly or implicitly) he or she did what they did; why the action made sense to them at the time. This is paramount to understanding the pathology of the failure. The action made sense to the person at the time they took it, because if it hadn’t made sense to them at the time, they **_wouldn’t have taken the action in the first place._**

### [What the Heck is a Relation? From Tables to Cartesian Products to Logic](http://merrigrove.blogspot.com/2013/12/what-heck-is-relation-from-tables-to.html?m=1)

This is a great blog about relations from a mathematical perspective, explained very well in layman's terms, which I found really helpful in creating a mental model for why relational databases are so darned good at modeling real world things.

### [Say NO to Venn Diagrams When Explaining JOINs](https://blog.jooq.org/2016/07/05/say-no-to-venn-diagrams-when-explaining-joins/)

It wasn't until I first read this article that I realized why the Venn Diagrams for JOINs are hard to remember: because they're wrong. Rather, this article explores using JOIN diagrams to explain JOINs, which is a much better way to think about them.

### [The Little Mocker](http://blog.8thlight.com/uncle-bob/2014/05/14/TheLittleMocker.html)

A great blog by Bob Martin on various types of test dummies, doubles, and mocks. A good read if you're into TDD.

### [Why Most Unit Testing is Waste](https://rbcs-us.com/documents/Why-Most-Unit-Testing-is-Waste.pdf)

While I'm a big fan of automated testing and TDD, it's important to understand the counterarguments. This blog makes a great case for balancing the cost of creating, running, and maintaining a test suite against the amount of risk it helps you mitigate.

> So when they wrote their first function for this project three years ago they wrote a unit test for it. The test has never failed The question is: How much information is in that test? That is, if "1" is the passing of a test and "0" is the failing of a test, how much information is in this string of test results:
> 
> 11111111111111111111111111111111
> 
> There are several possible answers depending on which formalism you apply, but most of the answers are wrong. The naive answer is 32, but that is the bits of data, not of information. You could be an information theorist and say that the number of bits of information in a homogeneous binary string is the binary log of the length of the string, which in this case is 5. But that isn’t what I want to know: in the end I want to know how much information I get from a single run of this test. Information is based on probability. If the probability of the test passing is 100%, then there is no information — by definition, from information theory. There is almost no information in any of the 1s in the above string. (If the string were infinitely long then there would be exactly zero bits of information in each test run.)

### [The Codeless Code](http://thecodelesscode.com/contents)

A collection of fictional stories - each of which is a metaphor for a programming lesson or problem, written in the spirit of Zen kōans. Some of my favorite entries are [The Tool-Shed](http://thecodelesscode.com/case/177) and [The Hidden Variable](http://thecodelesscode.com/case/124).

### [Never Heard Of It](http://alistapart.com/column/never-heard-of-it)

An article about learning to be honest about not knowing things, and in a profession characterized by constant change and learning, how to know which things are worth knowing.

> As I surveyed the patterns in my daily information bombardment, one dichotomy appeared rather quickly. Boiling it down to a quick litmus test: some things can be easily Googled for when needed, and some things cannot. This is a useful barometer, a differentiator between things to _reference_ versus concepts to _know_.

### [Programmer, Interrupted](http://blog.ninlabs.com/2013/01/programmer-interrupted/)

"A programmer loses X minutes of productivity when you interrupt them" is a common phrase that is bandied around in the programming industry - universally acknowledged, but tough to communicate to non-programmers and rarely backed up with research. This blog does exactly that: explains some research that demonstrates this to be true.

### [Joel on Software](https://www.joelonsoftware.com/)

Joel Spolsky was a very well-known blogger on programming and software design topics before co-creating the little-known website Stack Overflow. I thought about picking one article, but honestly the blog is filled with many gems and in my opinion any career programmer should read through it at least once. Even when I disagree with him, he explains his point well and in an entertaining way. Some highlights:

- [Designing for People Who Have Better Things To Do With Their Lives](https://www.joelonsoftware.com/2000/04/26/designing-for-people-who-have-better-things-to-do-with-their-lives/)
- [Bionic Office](https://www.joelonsoftware.com/2003/09/24/bionic-office/) "Private offices with doors that close were absolutely required and not open to negotiation."
- [The Development Abstraction Layer](https://www.joelonsoftware.com/2006/04/11/the-development-abstraction-layer-2/)
- [Two Stories](https://www.joelonsoftware.com/2000/03/19/two-stories/)
- [The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and character Sets (No Excuses!)](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)

### [Programming Sucks](https://www.stilldrinking.org/programming-sucks)

A humorous article that makes fun of the programming industry with a mix of metaphor and hyperbole.

> “Double you tee eff?” you say, and start hunting for the problem. You discover that one day, some idiot decided that since another idiot decided that 1/0 should equal infinity, they could just use that as a shorthand for “Infinity” when simplifying their code. Then a non-idiot rightly decided that this was idiotic, which is what the original idiot should have decided, but since he didn’t, the non-idiot decided to be a dick and make this a failing error in his new compiler. Then he decided he wasn’t going to tell anyone that this was an error, because he’s a dick, and now all your snowflakes are urine and you can’t even find the cat.

### [The Wisdom of James Mickens](https://mickens.seas.harvard.edu/wisdom-james-mickens)

Also known as "the funniest man at Microsoft Research" - his articles and presentations are unfailingly humorous, and he manages to mix his absurdist humor with pointed jabs at the state of the industry as a whole.

> In some way that I don’t yet understand, I’m glad that theorists are investigating the equivalence between five-dimensional Turing machines and Edward Scissorhands. In most situations, GUI designers should not be forced to fight each other with tridents and nets as I yell “THERE ARE NO MODAL DIALOGS IN SPARTA.” I am like the Statue of Liberty: I accept everyone, even the wretched and the huddled and people who enjoy Haskell. But when things get tough, I need mission-critical people; I need a person who can wear night-vision goggles and descend from a helicopter on ropes and do classified things to protect my freedom while country music plays in the background. A systems person can do that. I can realistically give a kernel hacker a nickname like “Diamondback” or “Zeus Hammer.” In contrast, no one has ever said, “These semitransparent icons are really semi-transparent! IS THIS THE WORK OF ZEUS HAMMER?”

* * *

More coming soon (tm) - as a find new blogs or remember ones that I think should be included, I'll add them here. Enjoy!
