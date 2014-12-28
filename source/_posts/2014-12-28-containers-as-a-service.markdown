---
layout: post
title: "Containers as a Service"
date: 2014-12-28 09:43
comments: true
categories: 
---
##28th December, Blog #4

##Containers as a Service

At a simple level, Infrastructure-as-a-Service deals with virtual machines, Platform-as-a-Service deals with applications, and Software-as-a-Service deals with users. I've [spoken a few times](http://blog.docker.com/2014/07/dockercon-video/) about Containers-as-a-Service(CaaS) - the idea that containers will become a new meaningful unit of currency in cloud computing. I've also [written about the ramifications of CaaS for PaaS](http://www.cloudcredo.com/pulling-paas-to-pieces/).

The hottest debate in the container ecosystem seems to be whether to use containers as single processes or multi-process virtual machines. The Docker folks seem to encourage the use of single process containers - a view I'm supportive of, following principles from software development, such as single responsibility and inversion of control. The alternative approach is to use containers as virtual machines with many processes. The virtual machine approach seems to resonate well with the current generation of operating systems and configuration management tooling.

I believe both approaches will continue to thrive for some time. The true value in Docker lies in the packaging and portability of containers, and this holds true whether you're packaging filesystems for a single process or a number of processes. Containers used as virtual machines will quickly erode the IaaS market - if only for their portability, speed, and density. Consumers and producers can gain benefits when choosing the CaaS abstraction over IaaS.

Over time there will be a move towards per-process containers, away from virtual machine-like containers, as the deployment and orchestration benefits from this approach become clearer. Just as SOLID, and TDD took time to gain momentum in software development so the correct patterns for containers will gain traction over time.

We will also see increasing numbers of customised operating systems, designed to run with the Linux kernel but providing a subset of the functionality, tuned for single-purpose containers. [OSv](http://osv.io/) is a great example of this. I also think we're likely to see an increasing number of container host OSs, presenting something that looks like a Linux kernel to hosted containers, under development. The boundaries between hypervisor and namespaced kernel will blur.

The other main areas for innovation will be storage and networking. Providing containers with reliable storage for mutable state is challenging. The ClusterHQ folks have made great progress in this area using ZFS-on-Linux in [Flocker](https://github.com/clusterhq/flocker). There are also exciting developments in the networking space from [SocketPlane](http://socketplane.io/) and [Weave](https://github.com/zettio/weave) - simplifying multi-host container networking.

CaaS solutions have already emerged from the big cloud players; you can easily host containers on GCE, AWS, and Azure. [Rancher](http://www.rancher.io/) looks to enable CaaS on any infrastructure. Pivotal's [Lattice](https://github.com/pivotal-cf-experimental/lattice) enables operators to deliver their own CaaS, as does its big brother Cloud Foundry. These solutions are currently largely focused towards Docker but I'm sure we'll see Rocket and alternatives emerge.

Whilst the future may look bright for containers, there are some warning signs. Multi-tenant container isolation and security are currently far from production ready. It also seems that choosing a layered filesystem beneath your containers can be a risky business; I've been bitten by few bugs.

I think CaaS will grow exponentially over the next few years. [Tutum](https://www.tutum.co/) are building the first pure CaaS I've seen. They attracted $2.65M in seed funding this year. I'm sure they'll have plenty of competition in the near future.

[Christmas Garage!](https://www.youtube.com/watch?v=02KRAshCG0w)