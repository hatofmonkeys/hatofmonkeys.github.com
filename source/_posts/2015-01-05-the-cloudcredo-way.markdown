---
layout: post
title: "The CloudCredo Way"
date: 2015-01-05 08:15
comments: true
categories: 
---

##[5th January, Blog #12](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/)

##The CloudCredo Way

Today, January 5th, is the last day of the twelve days of Christmas, so this is the last blog in [The Twelve Blogs of Christmas](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/). I survived. I may not have saved the best for last, but I've certainly saved the most important. This post is all about people, and how to get people delivering value. Great people make great things. Great things make great profit, or so I'm hoping.

###Explicit or implicit culture

This post is about growing the culture within my company, [CloudCredo](http://www.cloudcredo.com/), and the processes we use. I've spoken to many senior people in technology that believe you shouldn't tell developers how to develop, and should just let them get on with it. I firmly disagree with that opinion. I think a company should be clear about how you want to deliver value, and you will then attract people that 'fit' your culture. If you don't choose a way of working you are effectively saying "We let the senior staff bully the junior staff, code like cowboys, and do whatever they like.". But that's just my opinion.

I presented most of this content at [Extreme Programmers London](http://www.meetup.com/Extreme-Programmers-London/events/196398322/) and had a great response. I thoroughly recommend attending their meetups.

###Programming The Extremely Pivotal Way

I have been massively influenced by ["The Pivotal Way"](http://www.slideshare.net/motochan/agile-the-pivotal-way-compressed), in fact our working practices emulate it in most aspects. Imitation is the sincerest form of flattery. I had the tremendous good fortune to be invited to spend a few months in [Pivotal's Cloud Foundry Dojo](http://www.cloudfoundry.org/dojo/index.html) (I believe I may have been the first person through it) during CloudCredo's early days, which was an amazing experience. I've taken those learnings into CloudCredo and iterated on them.

We're using the processes to deploy and develop agile platforms and infrastructure - pair-programming test-driven development with our clients. We use the [Tracker](http://www.pivotaltracker.com/)-based planning process to empower authoritative product managers to prioritise bugs and features on multi-functional teams. You could call them 'devops' teams but I think that label has had all possible value eroded; they're teams focused on delivering business value. You write it, you run it.

###A process of feedback loops

I'm obsessed with fast feedback: I view the process as a set of shrinking feedback loops, making their way inwards towards the continuous feedback of pair programming, and expanding back out again. These loops are a good starting point until you find something that might work better. Have the courage to experiment. This content is *severely* abridged for brevity.

0\. Pre-inception - qualify readiness to start the process

1\. Inception - reach team consensus on a meaningful step forward, typically three about three months

2\. Iteration Planning Meeting - plan the next iteration, pointing

3\. Standup - today's work and pairs

4\. TDD (for design, refactoring, confidence, and numerous other reasons)

- Pairing (remove distractions, stop cowboy coding, skills transfer, and numerous other reasons)

4\. Acceptance - by an empowered product manager, the 'CEO of the product'

3\. Standup - helps/interestings/blockers from yesterday

2\. Retrospective - can we improve how we're delivering? The first derivative of delivery.

1\. Review - can we improve how we're improving on delivery? The second derivative of delivery.

###Why now?

Over the course of my career I've delivered many projects using a traditional "up-front architecture" approach, heavy on Gantt charts and light on prototypes. This was necessary when procuring servers (and the data centre space for them to live in) took months if not years. The cost of change for the infrastructure was massive; similar to changing the foundations beneath a skyscraper. The architecture needed to be right, and IT processes evolved around these assumptions.

The big change in our industry has been the increased agility of infrastructure. A six-month server procurement has become a thirty-millisecond container-starting API call. Infrastructure is now defined as code. The incredibly low cost of change means we can now use a process that embraces, rather than resists, change - and that process is [Extreme Programming(XP)](http://en.wikipedia.org/wiki/Extreme_programming).

###Why not Six Sigma?

Six Sigma is a fantastic methodology for eliminating defects and minimising deviation. Six Sigma is easy to implement with software: ``cp -ra``. It's less relevant when developing and running new services, where learning is more important.

###Why not Scrum?

Scrum and XP are both agile methodologies although I believe XP has a greater focus on learning. XP embraces change during sprints/iterations, Scrum favours commitments. XP is a more holistic process, recommending engineering practices such as TDD and pair-programming. As mentioned above, I see value in forming explicit opinions on these practices.

###Why not Kanban?

Tracker-based planning is actually a software-development-domain specific implementation of Kanban. Blur your eyes and you can see the swim lanes. Achieving and maintaining stable delivery flow is very important.

###Learning

As we're building and deploying new systems and services we need to embrace learning as we make progress. We're helping our clients to learn - and we're using a process that facilitates learning and embraces change based on that learning. Between competing organisations the organisation that can learn fastest, and channel its efforts in the right direction, will win. We learn through feedback loops such as [PDCA](http://en.wikipedia.org/wiki/PDCA), [OODA](http://en.wikipedia.org/wiki/OODA_loop) - both developments of [scientific method](http://en.wikipedia.org/wiki/Scientific_method).

The focus of XP is learning. Learn about what you're building so you can adjust your plans as you find out what's good and what's bad about what you're building. Learn about *how* you're building it; what's working and what needs adjustment. Use emergent velocity for data-driven planning.

###Supporting processes

There are a number of patterns we're using to support our chosen methodology. Here's a small selection:

- Continuous Delivery - start with a strawman (a test, a repository, a CI server) and continue delivering from there
- Microservices - people can't solve big problems: divide and conquer
- Release trains - continuously deliver all the things into an integration pipeline. If you want to 'tag' a release, run a release train through the last known good versions from the pipeline. Choo choo!

###Openness and communication

This information begs an obvious question: if this is CloudCredo's secret sauce, why would I blog about it publicly? This again comes back to XP, and two of XP's core values - courage and communication. I have the courage to lay CloudCredo's approach bare for all to see. If we're not working in the right way, or there's flaws, I hope they will be pointed out so we can improve. We're continuously trying to improve. Please [get in contact](http://www.cloudcredo.com/contact-us/) if you've got any feedback.

***

If you've been thoroughly confused by the UK Garage links at the end of all the [Twelve Blogs of Christmas](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/), well, maybe it's [a London thing](https://www.youtube.com/watch?v=obZIZWzlJa8).
