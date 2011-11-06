---
layout: post
title: "Automating Value"
date: 2011-11-06 13:26
comments: true
categories: 
---
I’ve always(well, for longer than my attention span) been a massive fan of outside-in development via BDD, in particular [Cucumber](http://cukes.info). Despite this affection I’ve thought it a little unusual that BDD frameworks ignore/discard the business value proposition stated at the beginning of a feature. It’s always felt like we’re saying “that’s too difficult to do anything useful with, we’ll leave that to the business idiots”. With that in mind, and being a business idiot, I’m going to attempt to construct a model for value and automate the testing of business-based assertions.

What I’m really trying to achieve is to extend the automated feedback cycle back into the business. The sooner the decision makers gain meaningful feedback about the impact of their decisions, the sooner they can start making useful decisions (and fewer useless ones).

I think this is where the devops camp needs to join forces with the [lean startup](http://www.amazon.com/Lean-Startup-Entrepreneurs-Continuous-Innovation/dp/0307887898) people (\*dev\*ops\*). I’m very interested in exploring if there’s any useful mileage in attempting to automate the [Deming Cycle](http://en.wikipedia.org/wiki/PDCA), and if there isn’t, to examine the reasons why.

![](http://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/PDCA_Cycle.svg/400px-PDCA_Cycle.svg.png)

Humans are great for the **PLAN** (hypothesise) phase, although I’ve heard and read some interesting thoughts around AI and entropy being used to automate this (Skynet++).

Devops and the associated tooling are great for the **DO** phase, and the [Continuous Delivery bible](http://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912) has had a massive impact here.

**CHECK** is often currently left either to chance or abstracted via some BI monstrosity. This is where I feel we need we may benefit from exploring automating assertions on business value. Most companies I work with have some capabilities around business metrics, but they’re infrequently linked back to the planning/strategic capabilities.

In theory an automated system can use some form of immunity metrics to roll back if the business assertions are not met, thus providing an element of automation around the **ACT** phase. I’ve seen a variety of immune systems employed around business metrics, however they often seem to be used as a tactical weapon rather than strategically to inform business decisions.

There are clear issues with attempting any kind of valid implementation, the obvious ones being around gaining useful feedback on a value proposition. From what I’ve looked at so far, automating value raises far more questions than it answers, but if we don’t push the boundaries on automating the feedback cycle then I feel we’re just locally optimising. I’ve had some really useful input from the folks at [OpenCredo](http://www.opencredo.com/), who are thinking along similar (but better formulated) lines, now I’m trying to actually make this concrete.

At the moment I’m working on extending cucumber, specifically on [“Lines 2-4 are unparsed text, which is expected to describe the business value of this feature”](https://github.com/cucumber/cucumber/wiki/Gherkin). I’d like to change this, making the business value executable (and testable) so we can assert the business value is being delivered as promised.

I’d like to change this

      Feature: Addition
        In order to avoid silly mistakes
        As a math idiot
        I want to be told the sum of two numbers

To this

      Feature: Addition
        In order to make 0 silly mistakes
        As a math idiot
        I want to be told the sum of two numbers

Or this

      Feature: Addition
        In order to make fewer silly mistakes
        As a math idiot
        I want to be told the sum of two numbers

And I want to assert that delivering this feature ensures the relative/absolute quantity of silly mistakes.

Attempting to write the code for this has made me realise how much time I've wasted in meetings of late rather than making myself useful, so if you’d like to lend a hand on the implementation of these ideas, please get in contact. I’ll post on this blog when I get the proof of concept up on the [Githubs](https://github.com/hatofmonkeys).