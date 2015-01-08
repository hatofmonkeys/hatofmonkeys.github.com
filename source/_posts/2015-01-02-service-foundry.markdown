---
layout: post
title: "Service Foundry"
date: 2015-01-02 10:58
comments: true
categories: 
---

##[2nd January, Blog #9](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/)

## Service Foundry

As I've mentioned a few times, [Cloud Foundry has won the Platform-as-a-Service(PaaS) war for stateless 12-Factor applications](https://twitter.com/swardley/status/527680598543187968). [Stateless PaaS will now be a Cloud Foundry distro war](http://blog.hatofmonkeys.com/blog/2014/12/30/paasaap-and-the-distro-wars/). [We all know mutable state is the root of all evil](http://blog.hatofmonkeys.com/blog/2015/01/01/mutable-state/) so I've been thinking about a stateful CF-like PaaS since I first interacted with Cloud Foundry. In fact, Cloud Foundry version 1 had an *interesting* service integration, which served to highlight the gaps in the PaaS journey for stateful application developers. [I tweeted a while back](https://twitter.com/hatofmonkeys/status/511856493512392704) about some of the work [we're](http://www.cloudcredo.com/) doing in this area; this post will expand on our plans for 'Service Foundry' - a PaaS for stateful deployments.

###Implementation

- [Docker/Rocket](http://blog.hatofmonkeys.com/blog/2014/12/03/docker/) for application packaging
- [Diego](https://github.com/cloudfoundry-incubator/diego-release) with mutexs for scheduling
- [Etcd](https://github.com/coreos/etcd)/[Consul](https://consul.io/)(reused from Diego's deployment) for service discovery
- [Weave](https://github.com/zettio/weave) to provide inter-container networking of clustered state
- [Flocker](https://github.com/clusterhq/flocker) for state relocation/replication
- [BOSH-IPSEC](https://github.com/CloudCredo/bosh-ipsec) for security of data in-flight
- HAProxy or custom Go router for non-HTTP routing
- Tunable sync/non-sync disk IO
- Expose STONITH semantics to users
- CF-like API for management
- TBC: [Kubernetes](https://github.com/CloudCredo/kubernetes-release) for clusters(pods) of containers

###Potential

It's interesting to consider that you could deploy Cloud Foundry itself in such a system. Does this actually look like a manifesto for BOSH version 2? Or does this look more like [OpenShift v3](https://github.com/openshift/origin)? The Kubernetes overlap certainly suggests something similar to [RedHat's latest IaaS+ effort](https://blog.openshift.com/announcing-openshift-origin-3/).

###Why is this useful to users?

I've given talks suggesting that [microservices and PaaS are the future of application development](http://gotocon.com/berlin-2014/presentation/Simple%20Scalability%20-%20Microservices%20on%20PaaS). Cloud Foundry makes it [incredibly easy to be tall enough for stateless microservices](http://martinfowler.com/bliki/MicroservicePrerequisites.html). I want users to have a similarly easy journey for the state powering their microservices.

If you'd like to help with this effort please do get in contact with [CloudCredo](http://www.cloudcredo.com/contact-us/).

***

[Christmas Garage!](https://www.youtube.com/watch?v=9yGT8QzVzKU)
