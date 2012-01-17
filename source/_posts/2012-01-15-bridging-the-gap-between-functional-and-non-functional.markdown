---
layout: post
title: "Bridging the Gap Between Functional and Non-Functional"
date: 2012-01-15 07:54
comments: true
categories: 
---
According to the [principles behind the Agile Manifesto](http://agilemanifesto.org/principles.html)

> Our highest priority is to satisfy the customer through early and continuous delivery of valuable software.

As I'm from an [operations](http://cache.blippitt.com/wp-content/uploads/2011/03/Mushroom-Cloud.jpg) background, I've always had great trouble communicating with the customer over requirements that have been relevant to my domain. The usual situation is that the "customer", often the product owner, views the working i.e. functionally complete software on a developer's machine, but bringing this to an operational service level is an afterthought (until it goes offline, and the real customers start complaining).

Traditionally, capturing these specifications has fallen under the umbrella of "non-functional requirements". As [Tom Sulston](https://twitter.com/tomsulston) pointed out to me, this suggests requirements that [aren't working](http://cache.blippitt.com/wp-content/uploads/2011/03/Mushroom-Cloud.jpg), which is precisely the opposite of what we're attempting to express.

I've sought to tackle this in a couple of ways.

1. Spread FUD throughout the non-technical customer base.
    - "Do you want it to explode?"
    - "NO!"
    - "Well you should ask for non-exploding software in your stories then!".

2. Get the team in a room together and express "cross-cutting concerns" (I [half-inched](http://www.cockneyrhymingslang.co.uk/slang/half_inch) the idea from [AOP](http://en.wikipedia.org/wiki/Aspect-oriented_programming)) that span the project as a whole.

I haven't been happy with the results of either approach, so I'd be interested to talk to anyone with a satisfactory solution in this space.