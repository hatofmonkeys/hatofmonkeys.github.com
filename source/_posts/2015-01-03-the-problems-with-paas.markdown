---
layout: post
title: "The Problems With PaaS"
date: 2015-01-03 07:59
comments: true
categories: 
---

##[3rd January, Blog #10](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/)

Platform-as-a-Service(PaaS) isn't perfect. There are always going to be some things it does well and some things it does badly. This post takes a look at some of the things it does badly, and how we can make improvements in the future.

###Stateful services

[This excellent article](http://compositecode.com/2013/07/27/architectural-paas-cracks-or-crack-paas/) highlights some key points related to problems with PaaS. I absolutely agree that the data service journey with current implementations is painful. I've written about [CloudCredo's](http://www.cloudcredo.com/) plans for ["Service Foundry"](http://blog.hatofmonkeys.com/blog/2015/01/02/service-foundry/); this is work-in-progress and needs to be an area of greater focus. Stateful services need to become first-class citizens in the PaaS landscape.

###Maintenance troubles

I also agree that maintaining PaaSs is currently too difficult. I think this is a symptom of two separate issues. Firstly, the current crop of configuration management tools (Chef/Puppet/Salt/Ansible etc.) are not fit for the purpose of deploying and maintaining distributed systems, such as PaaSs. Secondly, [BOSH](http://bosh.cfapps.io/) is the right tool for the job but currently has a difficult user journey. [CloudCredo](http://www.cloudcredo.com/) have invested time and effort attempting to make BOSH easier to consume - but again it's another work-in-progress. We need to get better at making PaaSs easier to operate, maintain, and upgrade.

###Secure networking

[Another good blog post](https://medium.com/p/817849715f0a) highlights how networking concerns can block PaaS adoption. Since the writing of that post a couple of advancements have been made. There is now an [easily consumable BOSH release to enable encrypted network traffic of any BOSH-deployed service](https://github.com/CloudCredo/bosh-ipsec) - [although we should always question how secure our encryption is](http://www.spiegel.de/media/media-35515.pdf). There is also [user-configurable networking inside Cloud Foundry](http://docs.cloudfoundry.org/concepts/security.html). I believe these additions go a long way towards mitigating user concerns, but I'd certainly be interested in further feedback related to PaaS networking.

###Transparency

The greatest strength of PaaS is that it's a black box for running your applications; it allows developers to focus on delivering value rather than operating a platform. The greatest weakness of PaaS is that it's a black box for running your applications; when things go wrong it can be difficult to work out what's happening. If you application is performing poorly on Heroku, what do you do next? Spend more money and hope? [Cloud Foundry's new Firehose](http://www.cloudcredo.com/cloud-foundry-firehose-and-friends/) generates huge volumes of information but can prove difficult to consume for PaaS novices. [Buildpack integration with monitoring systems](http://blog.newrelic.com/2014/10/27/cloud-foundry-java-buildpack-new-relic-2/) is clearly helpful but we could still make enhancements in this area.
 
###Let's keep PaaS-bashing

PaaS will only improve if we identify and expose the flaws. We need more users, more critiques, more real-world scenarios. Please [get in contact](http://www.cloudcredo.com/) if there's any burning issues blocking your adoption of PaaS.

[Christmas Garage: London - Stand Up Tall!](https://www.youtube.com/watch?v=L3HMogp86cI)
