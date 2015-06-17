---
layout: post
title: "The Future of BOSH"
date: 2015-06-16 14:16
comments: true
categories: 
---
I [love BOSH](http://blog.hatofmonkeys.com/blog/2014/03/15/configuration-management-isnt-stupid/). I have many conversations with people about where BOSH is going so I thought it a good idea to capture my thinking in a post. This post.

###Two Options

1. BOSH deploys and manages all the things. It's the best distributed-system-system I've ever used.

2. BOSH should be the deployer of Diego and other container schedulers.
    - Diego et al deploy and manage all the things.
    - Diego becomes something like [Service Foundry](http://blog.hatofmonkeys.com/blog/2015/01/02/service-foundry/).
    - The world is a better place because non-[12-Factor](http://12factor.net/)-app developers have a contract to develop to, and the fast-feedback of container-driven deployments.

I currently favour option 2 but reserve the right to change my mind as I learn over time. Previous attempts to build multi-purpose stateful/stateless PaaSs haven't gone *amazingly* well. If you're building a stateful service right now, build it for BOSH, not Diego.

###What Next?

We'll be exploring the cool new future of Diego in a [LoPUG hack day](http://www.meetup.com/London-PaaS-User-Group-LOPUG/events/222965597/) and looking at ideas like a Diego CPI for BOSH, persistent disks, and TCP networking in PaaS. Join us to find out more.
