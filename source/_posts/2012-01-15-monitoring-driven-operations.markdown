---
layout: post
title: "Monitoring-Driven Operations"
date: 2012-01-15 08:11
comments: true
categories: 
---
**RAMBLING BLOG POST ALERT**

Monitoring sucks.

Following the "if it hurts, do it more often" mantra that has driven the success of patterns such as [Continuous Delivery](http://continuousdelivery.com/), there might be some value in jumping head-first into the world of monitoring.

I've been [evangelising](http://www.eatliver.com/img/2005/638.jpg) to anyone that will listen, and a lot of people that won't, about declarative/convergent frameworks for some time now. Sometimes you have to describe how to converge (definitions may not yet exist), so I particularly enjoy working with frameworks such as [Chef](http://wiki.opscode.com/display/chef/Home) that enable you to easily move from declarative to imperative as the need arises.

These two trains of thought(monitoring + system convergence) collided a while back to make me think about Monitoring-Driven Operations, i.e. that we can declare the status of the monitoring systems (that servers and services are available during expected hours) and converge the environment(s) on this desired state if there's a gap between observed and desired states. MDO for operations, TDD for developers.

It turned out I [wasn't alone](http://dev.hubspot.com/bid/65871/Monitoring-Driven-DevOps) in thinking about monitoring from this perspective.

Reusing the application behaviours in production is a natural, logical extension of [the testing pipeline](blog/2011/11/13/the-testing-pipeline/). Were we able to ensure that the [behaviours include non-functional requirements](blog/2012/01/15/bridging-the-gap-between-functional-and-non-functional/), would it be possible to use these monitored behaviours to converge an environment towards a state that passes all scenarios?

The missing link here is the imperative element. We can declare the desired state for an environment ([cucumber-nagios](http://auxesis.github.com/cucumber-nagios/) is a good start), however we need a framework to express *how we get there*. I think Chef/Puppet can help with a lot of the hard labour here, but I don't think that either, in their current formats, are appropriate to converge a service from a failed monitoring check.

[Cloud Foundry](https://github.com/cloudfoundry/)(brilliant) uses a health manager, message bus, and cloud controller interacting to accomplish something similar. In this situation the cloud controller knows how to converge the state of the environment when the health manager observes a disparity between observed and desired states.

I'm thinking about developing a system that works in the following way("*The Escalator*"). Please get in contact if you've got any feedback.

* Barry McDevops declares an escalation pattern for his environments. These are the *levels* of escalation for convergence that failing checks can be matched to. As a crude example:
    1. Create account with IaaS provider
    2. Create core networking and support infrastructure
    3. Create tier networking and all VMs
    4. Create an individual VM
    5. Converge VM with Chef
    6. (Re)deploy application
* Barry creates a series of monitoring *checks* for the non-functional requirements
    1. IaaS provider is online
    2. (per node) ICMP ping reply
    3. (per node) app and DB services are online
    4. (per tier) app and DB services are online
    5. Smoke check of application
* Barry maps each monitoring *check* to an escalation *level*
    - Check 1 => Level 1
    - Check 2 => Level 4
    - Check 3 => Level 5
    - Check 4 => Level 3
    - Check 5 => Level 6
* Once engaged, the monitoring system will quiesce for 30 seconds, observe the highest level of required escalation, and then ask the escalation system to take that level of action (and all levels below it).

As examples:
- If there is nothing in place (failed IaaS provider or a new system) - an entire new environment is built from scratch (escalation steps 1 through 6).
- If a node fails: a new node is built, converged, and deployed to (steps 4 through 6).
- If the application fails the smoke test, the application is redeployed (step 6).

Obviously it is up to Barry to ensure his escalation steps are sensible, i.e. use multiple IaaS providers, redeploy previous versions of applications if they persistently fail smoke tests. Each escalation step should declare a quiescence period, during which no further actions will be taken. There's no point attempting to deploy an application if you have no nodes.

If an escalation process fails, the monitoring system could attempt a re-convergence if necessary or contact an administrator.

This overlaps significantly with a couple of discussions: [here](http://wiki.opscode.com/display/chef/Cluster+Orchestration) and [here](http://wiki.opscode.com/display/chef/Management+of+External+Entitites) at the recent [Opscode Community Summit](http://wiki.opscode.com/display/chef/Opscode+Community+Summit+1), so perhaps someone else is already creating something similar with Chef.