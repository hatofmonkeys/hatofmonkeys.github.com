---
layout: post
title: "The Testing Pipeline"
date: 2011-11-13 11:11
comments: true
categories: 
---
I was fortunate in being able to attend [Citcon](http://citconf.com/london2011/) this weekend and met some wonderful, talented people. I proposed a couple of openspaces, one loosely based on [automating value](blog/2011/11/06/automating-value/) and the other around test reuse.

I've been thinking for a while about how I see people (including myself) rewrite the same business logic in our behavioural specifications, for our integration tests, for our performance tests, for our security tests, and for our behaviour-driven monitoring. This seems counter-intuitive to someone as lazy as I am.

I think we should reconsider the deployment pipeline as a testing pipeline. The purpose of the pipeline is to increase confidence in the release candidate as the stages are passed. These stages can be considered as hoops for the release candidates to jump through. As new functionality is added, so the hoops will need to be tailored to ensure the new functionality is fit for purpose.

Here's an idea of a delivery pipeline I've seen used many times before. It's in no way ideal, nor suitable for every use case, but it provides an example for discussion:

Behaviours(product owner) -> unit(dev) -> **code**(dev) -> VCS -> unit tests(CI) -> behavioural tests(UAT) -> load tests(staging) -> security tests(staging) -> monitoring(production)

The issue I'm attempting to highlight is that as desired functionality is added by the product owner (typically as a feature in the backlog) and committed to a release candidate by the developer, so the hoops need to ensure that the new functionality is delivered as specified, and no regression bugs have been introduced. This typically involves either the new functionality going untested through load/security/monitoring, or a developer/operations person having to rewrite the new business logic repeatedly in the DSLs of whichever tools are used to create the hoops.

I'm currently using [cucumber-nagios](http://auxesis.github.com/cucumber-nagios/) to reuse our functional behaviours for monitoring and I've also had some success using [PushToTest](http://www.pushtotest.com/) with Selenium from Cucumber. I've yet to look at how to tackle security requirements. Please get in contact with me if you've had any success reusing your business logic assertions throughout your pipeline; I'd be very interested to hear about your experiences.

My (current) vision would be that, either as a part of or along with a release candidate, an artefact is created that outlines the business value assertions made about the candidate. As the candidate then moves through the pipeline, so the hoops are updated with the relevant assertions they need to test about the candidate. These could be a certain number of virtual users through the user journeys in the expected ratios, lack of injection holes in the application, the application's ability to degrade gracefully through various failure modes, and anything else that's required to establish confidence in the release candidate.

You should be able to make an API call to cloud-based testing providers(such as [Soasta](http://www.soasta.com/)) so they can use your artefact to automatically test the behaviour of your application, such as external load and security tests. The feedback from these providers can be returned to your CI server for tracking over time, and form a basis for diagnosis of any assertion failures.

Without a fully-automated testing pipeline, I see one of two outcomes regularly at the moment:

* New functionality is not tested before release. This implies risk.
* Releases are delayed while scripts are updated, and manual load/security tests booked with vendors and executed. This inhibits business agility and delays feedback cycles.

I'm attempting to write an abstraction layer for Cucumber scenarios to be reused in load tests, if you're interested in helping please get in touch. I'll post it on the [Githubs](https://github.com/hatofmonkeys) once I've got something small working.