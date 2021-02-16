---
title: "Your Agile Transformation Failed Because You Didn't Want to Succeed"
author: Shawn
date: "2021-02-15"
categories: ["Programming"]
tags: ["Agile"]
---
## "We're Adopting Agile!"
This is a common refrain among modern software organizations. Agile is the future! It's time for us to change! We're going agile, baby!

Yet often times, the adoption doesn't go so well. The developers eventually find that these promises were hollow - they grumble in retrospectives that the organization hasn't actually put the agile principles into practice. After a year or so, the only lip service paid to "Agile" at all is some burndown charts in your backlog and a daily standup where you used to actually stand up back before COVID sent us all to our home offices.

So what happened? Before we get into why you failed, let's talk about what you wanted to succeed *at*. Let's dispense with Scrum or Kanban or Extreme Programming - any particular flavor of Agile - and talk about Agile itself, the idea that spawned all of the many Agile processes.

## Agile

The Agile manifesto is actually quite simple - just a values statement, really. You can read it in its entirety below, as it is captured on agilemanifesto.org.

![Agile Manifesto](/content/2021/02/agile-manifesto.png)

It's so simple... and obviously good! Why didn't it catch on in your organization?

## You Didn't Want to Succeed

It's a tough pill to swallow, but this is almost certainly the root of it. Your organization, quite simply, valued the things on the right more than the things on the left, and wasn't prepared to change its organizational values.

You valued "following and iterating on the process" over empowering individuals to interact pragmatically and organically.

You valued "let's make sure this whole process is added to the documentation" over putting working software in front of users and collecting their feedback to ensure that its UI was so intuitive to them that it needed little documentation.

You valued "this is what the customer asked for, it's right here in the contract" over delivering software that meets and exceeds the customer's actual expectations.

You valued "creating and reliably delivering on our (3, 6, 12, 24 month) plan" over the humility of admitting that in many cases, you simply don't know what the customer wants until they see it and say "that's perfect, I love it!"

This is akin to saying that you want to travel to Hawaii but are afraid of heights and won't take an airplane. It is, I suppose, still possible to get to Hawaii - but don't expect to be making the trip in under 24 hours. If getting there quickly is important to you, then it's time to start working on overcoming your fear of heights.

Many organizations have members, or sometimes customers, with significant political or actual power who truly do value these things over "agile." They want a *plan*, they need to know before the software exists what they're *getting* so they can provide a *forecast* and sell the contract to their board of directors who view software as an assembly line and whose familiarity with Agile is a puff piece they read in Forbes one time.

When the people who determine your business priorities truly value the things on the right more than the things on the left, as is the case in many organizations, a so-called "agile transformation" will only ever succeed in bringing in a few dozen Agile terms and rituals and scattering them into the spaces between your business's existing Very Important Processes.

## Then Why Attempt Agile at All?

Because software organizations who successfully adopt Agile practices are often very successful as a business. Your organization's leaders saw other organizations singing the praises of Agile - how their software quality improved, customers raved about the results, productivity improved, employee turnover dropped. They became an industry leader practically overnight!

They want those *results* but they are [Cargo Culting](https://en.wikipedia.org/wiki/Cargo_cult) - they don't understand the fact that these results stem from a fundamental change in the organization's values and approach to software development.

Standing up and capping your meetings at 15 minutes, measuring velocity, breaking work into short sprints, having a colorful backlog - these are unimportant on their own. They are simply tools used to accomplish a *goal* and those who percieve programming as an assembly line of "features" don't understand the goal itself.

## What is the Goal of "Real" Agile?

The Agile values all stem from a realization that experienced software practitioners came to amidst the .com bubble and the advent of home computing - the process of software creation is a relationship between two types of people: Problem-Havers (the customer/user) and Problem-Solvers (the software team.)

That's really all it boils down to - people don't actually care about software at all. If I could do everything I do with my computer faster and easier with a magic wand, I'd never power on my PC again. I use software because it *solves* my *problems*. You do, too. This is the relationship we all have with software.

I log onto Facebook to see what my friends are up to, not look at their funny emojis. I open Excel to answer some question I have by organizing data, not because of Excel's riveting user interface. I send an email because I want someone who's 2,000 miles away to know something that I can tell them with text, not because email is such a blast to use.

This relationship is not unique to software at all, in fact - virtually all professions arose as the solution to a problem. I call a plumber (Problem-Solver) because my sink is leaking, which has suddenly turned me into a Problem-Haver.

If the plumber arrived at my house, looked at the leaky sink, then recommended replacing my cabinets, I wouldn't be very pleased. The cabinets may be *nice*, sure - they also come with extensive documentation and a 5-year warranty. Maybe it's even in his company policy to try to upsell customers on new cabinets - he's sticking to The Plan like his boss told him to! But they don't solve my problem.

If I became impatient and asked him to just replace the U-bend and he did it and left, but the leak didn't stop because it wasn't in the U-bend, he wouldn't get points in my book for *following the plan* and *sticking to the contract* because... he didn't solve my problem! I was paying him to make my problem go away! I never cared about the cabinets or the U-bend or any of this, I just want a sink that doesn't leak!

Fix problem! Magic wand! I'm offering money for solutions here!

## Where Agile Comes In

Agile stems from this realization - that in order to solve problems their causes and solutions must be understood. Which means that an effective feedback loop *must* exist between the Problem-Havers and the Problem-Solvers in order for the result to be software which effectively resolves the problem.

Furthermore, you can't naively ask the customer for a list of features they want - they may ask you to replace a U-bend when the leak wasn't in the U-bend. Most people who have problems don't understand them deeply, or even want to - they just want them to go away! You're the expert, figure it out! They're paying good money for solutions here!

Consider a clock app. It just shows the current time. Couldn't be simpler. Right? Well...

<iframe width="560" height="315" src="https://www.youtube.com/embed/-5wpm-gesOY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Turns out that time is actually pretty complicated. What time it is depends on where you are. And also what time it is. Sometimes 1:01am happens twice in one day. Sometimes it never happens at all. But only in certain places on Earth. What about 24-hour time? Leap years? Leap seconds? The International Date Line?

Things that seem simple rarely are, and programmers' job - the real job - isn't to merely write code, but to learn to deeply understand real-world problems and then figure out how to use code to solve them.

So Agile grapples with this reality by acknowledging that at beginning of the problem-solving process, it is most likely the case that the person whose problem is to be solved by the software doesn't actually understand it much better than the development team who is also unfamiliar with the problem. Furthermore, they are probably not familiar with UX best practices, or what technology exists that could help solve their problem.

Thus the starting point of any software project is simply to collaborate with the Problem-Haver to identify what the root of the problem actually is, even when they don't understand it and can't fully articulate it themselves.

## The Dreaded Pivot

Not only that, but even if they were savvy about the software process amd diligently prepared a list of use-cases and feature requests for you, there are almost certainly important constraints and use cases that they will never mention until they see working software right in front of them that *fails* to meet them.

"I'd like to see how that looks on my iPad! Oh, wait - this doesn't have a mobile app? I mean the computer is fine for demos and all, but all my employees will be using this on iPads in the field. It *has* to run on an iPad. Without internet - they don't have internet out there a lot of the time. I thought this whole desktop app thing was just a mockup - we'll never actually use it on Windows. You can just port it, right? Isn't everything mobile compatible these days?"

Oh. Well, there went our plan to build a desktop app. Good thing we weren't too worried about 6-month forecasts and are focused on solving the customer's problem, right?

This is an amazing opportunity to realize more customer value with our final product thanks to really important new information we got from a design review meeting with a client! ...Right?

Knowing these things about their use-cases and problem domain will give us a competetive edge over our stuffy competitors who don't collaborate with their users like we do!!

...Right?

Or was that 6-month plan important to you? Or to someone who asked you for it?

No, of course not! We're Agile! We are prepared to pivot!

Just... uh... let me call a big stakeholder meeting, draft emails to 2 big message groups, update half a dozen pieces of documentation and team forecasts, schedule 3 full days of planning next week to draft the new 6-month plan, and then send a carefully-worded message up to the Board that there's been a - ahem - *change* to our Q3 deliverables (\*cough\* It'sGonnaBeAMobileAppNowAndWe'reScrappingTheDesktopAppEntirely \*cough\*)

Yeah, your organization isn't ready for Agile. You, or the people with clout in your organization, care about the stuff on the right more than the stuff on the left.

## Sometimes That's How It Has to Be

You may be operating in a field where existing constraints prevent you from actually operating in an Agile manner. Good luck pitching a 2-year contract to a government agency that has to secure funding from 16 layers of bureaucrats without actually giving them a feature list and some mockups. With some customers you *need* the contract and the plan.

There may be practical, financial, or political constraints within your industry that prevent you from taking a properly Agile approach to software development. The results will be correspondingly worse of course - users working around features instead of loving them. Design-by-committee UIs. Voluminous help documentation that no one ever reads. This isn't an amazing way to work.

But sometimes those are the constraints you have to work under.

But if those are your constraints, and the values that matter to the people who matter in your organization are not Agile values - then draping some Agile rituals over your existing processes won't yield anything of value for you.

Your organization's Agile transformation will fail because you don't want it to succeed.