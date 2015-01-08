---
layout: post
title: "Mutable State"
date: 2015-01-01 13:03
comments: true
categories: 
---

##[1st January, Blog #8](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/)

##Mutable State

I enjoy attending developer-focused conferences - in particular [QCon](http://www.qconferences.com/) and [GOTO](http://gotocon.com/) - to talk to the real consumers of PaaS. I also attend infrastructure-orientated conferences as a consumer of IaaS. I was recently on the PaaS panel at the [Apache CloudStack Conference](https://twitter.com/VirtualBlackCat/status/535433555271495680) when I made what seemed a bizarre statement to many in the audience: "If your problem isn't mutable state then you're probably doing something wrong.". I'm taking this opportunity to explain what I meant.

###Mutable state is the problem

I've actually been making statements in this vein for a long time. In my experience, when delivering solutions, you can usually find a *correct* answer to your problem, given time to research and engineer sufficiently. The majority of optimisation problems have occurred when I've been facing issues related to mutable state. These generally involve functions related to latency, consistency, availability and performance. [CAP theorum](http://en.wikipedia.org/wiki/CAP_theorem) is perhaps the most frequently occurring; choose availability or consistency in the face of network partitions in a distributed system. You cannot have both. 

###Development

Approaches to mutable state vary across programming paradigms. Object-orientated programming favours encapsulating mutable state in objects; usually controlling concurrent access to the mutable data via mutexs or semaphores. In my experience this can lead to heavy performance issues when scaling. Functional programming favours having no mutable state; instead passing immutable values between functions. This causes different issues as it shifts the burden to the developer to model their data - in what can sometimes be an unnatural way.

###Infrastructure

Mutable state in Infrastructure-as-a-Service can also cause issues. VMWare's various infrastructure offerings favour a consistent view of the infrastructure landscape, often using Oracle or MSSQL as an ACID-compliant database for consumers to rely upon. This makes the API easy to consume but difficult to scale to huge levels for producers. Consumers can rely on their mutations being immediately reflected across the API.

AWS EC2 offers an eventually consistent view of their landscape. This means EC2 can be delivered at a truly unprecedented scale but can cause issues for [platform-level consumers](http://blog.cloudfoundry.org/2013/06/18/dealing-with-eventual-consistency-in-the-aws-ec2-api/). Intelligence must be built into the tooling that consumes the API, as large consumers of EC2, such as Netflix, have done. 

###Platform

At a Platform-as-a-Service(PaaS) level we have tended to deal with the issue of mutable state by abdicating it to external services. Stateless application hosting is a done deal - [Cloud Foundry has won that battle](https://twitter.com/swardley/status/527680598543187968). Stateless application developers can choose to locate their data in whichever external service best suits the data; this is the polyglot approach embraced by PaaS. The real issues arise when we attempt to provide a Cloud-Foundry-like journey for developers and operators around stateful services.

An increasing number of PaaS developers appear to have become preoccupied with scheduling. Scheduler debates are so hot right now. No PaaS conference would be complete without an [Omega-style optimistic scheduler versus Mesos-style pessimistic scheduler conversation](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/41684.pdf). In my experience scheduling performance is rarely the constraint blocking PaaS adoption: the constraint is usually dealing with the necessary mutable state generated/consumed by the applications running in the PaaS.  

###Two PaaSs to rule them all?

[RedHat recently stated that dividing stateful and stateless services "is an arbitrary distinction".](https://blog.openshift.com/chose-not-join-cloud-foundry-foundation-recommendations-2015) I don't agree with this perspective; I think it's a very important distinction. There are some key issues here - if an application container appears to have stopped functioning, what action should the PaaS take? If the container is stateless the PaaS can request a new container be started: potentially creating a duplicate. If the container is stateful the choice is more complicated. Should a new container be started, maximising service availability, but risking split-brain scenarios in a stateful environment? Should the container remain offline, reducing availability but ensuring data consistency? Should the container be restarted following a successful [fencing](http://en.wikipedia.org/wiki/Fencing_%28computing%29) operation? What does fencing look like in a distributed, scheduled, containerised PaaS environment? These questions may lead to a separate breed of stateful PaaSs emerging focusing on stateful concerns, even if they share similar-looking APIs.

```
cf push mysql/mysql --disk 500 --restart-policy consistent  --disk-sync immediate --io-performance high
cf push redis/redis --disk 100 --restart-policy available --disk-sync defer --io-performance medium
```

###BOSH

The "Two PaaS" debate has led to some people perceiving Cloud Foundry as a stateless PaaS and BOSH as a stateful PaaS. I believe this is an incorrect interpretation. I think BOSH is a fantastic system - it has had a greater influence on me than Cloud Foundry itself - but it is not a PaaS. BOSH is the purest embodiment of the principles of Infrastructure as Code: it fires up metal, lays down code, and attaches disks for state. It is not, in its current form, a scheduler in the manner of Mesos/Omega. BOSH is the world's best deployer of schedulers and distributed systems. A stateful PaaS would look more like [Diego](https://github.com/cloudfoundry-incubator/diego-release)/[Lattice](https://github.com/pivotal-cf-experimental/lattice), modified to address the concerns above. BOSH would be a great way to deploy this new PaaS.

***

[Christmas Garage!](https://www.youtube.com/watch?v=hQilwacuBO0)