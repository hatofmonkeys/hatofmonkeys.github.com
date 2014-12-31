---
layout: post
title: "Multi-Site Cloud Foundry"
date: 2014-12-31 10:20
comments: true
categories: 
---

##[31st December, Blog #7](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/)

##Multi-Site Cloud Foundry

[CloudCredo's](http://www.cloudcredo.com/) clients often ask about how to run Cloud Foundry across multiple sites for performance and resilience. This is a natural question to ask: as an application developer, if I specify that I need to have ten instances of my application available, I expect ten instances to be available - whether the underlying infrastructure is available or not. The Platform-as-a-Service(PaaS) abstraction implies that my application should continue to run as desired, and that the PaaS should be designed to handle failures in the infrastructure layer.

###Choosing a CAP

This idea sounds great in theory but can lead to some problems in practice. What should Cloud Foundry do, as a distributed system, in the event of a network partition? Should each partition converge on the desired state of the whole system, leading to twice the number of applications being online, and potential split-brain issues with singleton applications? Should the whole Cloud Foundry shut down to ensure application consistency? The key point to note here, which is not immediately obvious, is that whilst Cloud Foundry hosts *stateless* applications, it is actually a *stateful* system itself. This means [CAP theorem](http://en.wikipedia.org/wiki/CAP_theorem) must be obeyed; we can opt for consistency or availability in our Cloud Foundry deployment.

Cloud Foundry has, at its core, a Cloud Controller database maintaining the desired state of the system. If we maintain a single, consistent state of this database we will be running a CP(consistent, partition-tolerant) Cloud Foundry. If we allow multiple, divergent copies of this database we will be running an AP(available, partition-tolerant) Cloud Foundry.

###Consistent Cloud Foundry

Cloud Foundry's current engineering direction seems to favour a consistent view of the desired application state. This is exhibited by the choice of [Raft](http://en.wikipedia.org/wiki/Raft_%28computer_science%29) as a consensus algorithm, and [Etcd](https://github.com/coreos/etcd) as an implementation, for CF's next generation [Diego](https://github.com/cloudfoundry-incubator/diego-release) components. These choices pose some difficult questions:

- Do we suffer thundering herd issues in the event of a network partition, where all desired instances of all applications attempt to run on the nodes with access to the quorate Etcd partition?
- How do we ensure data services, required by the applications, are accessible from the functioning side of a partition?
- How do we ensure latency to data services from across multiple sites does not reduce application performance below acceptable levels?
- What happens if the Cloud Foundry components themselves experience issues, degrading the service as a whole across all sites?

Running a consistent Cloud Foundry makes application deployment and management very easy; there is a single API endpoint for management. At CloudCredo we deploy consistent Cloud Foundry installations across multiple availability zones within a single region. This mitigates the latency concerns and provides a convenient management structure for application deployment.

###Available Cloud Foundry

When I've needed to deploy Cloud Foundry across multiple regions it has usually been to provide for a very high availability service level. To provide for this I have deployed multiple, completely separate Cloud Foundry installations, often on heterogeneous infrastructure providers, in diverse regions. An example of this kind of installation would be the [donations platform for Comic Relief](http://blog.cloudfoundry.org/2013/04/30/uk-charity-raises-record-donations-powered-by-cloud-foundry/). The huge benefit of this strategy is that no outages in any individual Cloud Foundry can stop the service - availability is maximised. The two major downsides are that deployment and orchestration of applications becomes significantly more complex, and that the applications and data services need to be developed to handle being deployed in a distributed system of this nature.

###The Perfect Cloud Foundry?

I'm currently deploying multi-zone 'consistent CF' - and then multi-region 'available CF' if requirements demand it. This is a domain specific choice; and it takes a significant amount of work in the application(particularly around state) to bring multi-region availability.

[Christmas Garage!](https://www.youtube.com/watch?v=RQLQ7W2RoKA)
