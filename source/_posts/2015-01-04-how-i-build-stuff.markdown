---
layout: post
title: "How I Build Stuff"
date: 2015-01-04 08:06
comments: true
categories: 
---

##[4th January, Blog #11](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/)

##How I Build Stuff

This is likely to be the most nonsensical of my thoroughly nonsensical [Twelve Blogs of Christmas](http://blog.hatofmonkeys.com/blog/2014/12/25/the-twelve-blogs-of-christmas/). I wanted to capture the recurring themes of the processes I've employed when bringing software to life; from inception to massive scale. Everything here should be overridden by domain-specific knowledge/concerns as appropriate. Or ignored altogether :)

###Don't build anything

If you've had an idea for something, it's probably already been done. Go and have a look. If your idea hasn't been done it's probably quite likely you can reskin/resell/repackage/repurpose a current service to deliver the new service you're hoping people will find valuable.

###Start at the top, not the bottom

If your idea hasn't been developed before, look for two or more currently running services you can combine to create the value. Use SaaS. If you have to write software, host it in a PaaS that does as much heavy lifting as possible. Don't start with infrastructure and build upwards. You don't have time, and you've got better things to do.

###Get feedback from day 1

Get meaningful feedback about your service as soon as possible. Your idea is probably stupid, and you should stop (or pivot). That's the harsh reality of the situation. Continue getting feedback about your decisions as fast as possible and as frequently as possible. Your ability to gain and act on feedback will be the key determinant of the success or failure of whatever you're building. Read 'The Lean Startup'. [Cucumber-value](https://github.com/hatofmonkeys/cucumber-value) is a rubbish piece of software, but should make you think about how you can quantify and measure real metrics for success.

###Use small teams that 'own' services with business value

Business services are owned by small teams. Teams own one or more (micro?) services. Use [Domain-Driven Design](http://en.wikipedia.org/wiki/Domain-driven_design) as a guide for breaking large problems into smaller services. Don't overly engineer towards microservices, let them emerge, you can break them down further at a later date. Don't be afraid to sacrifice your architecture if it needs replacing; you're learning. Hire people that learn fast; they can gain knowledge from others in the team. Use ['The Pivotal Way' - lightweight XP](http://www.slideshare.net/motochan/agile-the-pivotal-way-compressed). Initially create a Git repository per service; shared code will emerge into new repositories. Use GitHub or BitBucket - you're not a Git hosting service (unless that's your idea, and if it is, it's already been done). 

###Deploy to somebody else's Cloud Foundry

Deploy two(or more) Cloud Foundry instances per (micro)service. Use run.pivotal.io, Anynines, Fjord IT, AppFog, Bluemix, or any other hosted Cloud Foundry (not your own). Write and deploy your (micro)services quickly, in languages you can develop quickly in: we like Go and Ruby. If you need to develop in a less agile language as requirements emerge you can do that later. Don't be afraid to use a range of languages; the cost of doing this is mitigated by the PaaS abstraction. Kill your (micro)services and create new ones as necessary.

###Start with Continuous Delivery and continue to deliver

Begin with a test for 'Hello World', an app that outputs 'Hello World' in your chosen language/framework, and a CI server that can run your test then deploy the working software to Cloud Foundry. Iterate from there. Use Travis or Circle until you need your own Jenkins/GoCD/Concourse solution.

###Log problems and measure latency

Log when things go wrong. Measure the latency(time from request to response) when things go right. Use Papertrail for the logs. Use New Relic for the metrics. Replace Papertrail with [Logsearch](https://github.com/logsearch) and New Relic with Graphite when you need to.

###Use JSON templates

Use JSON to communicate between your (micro)services. Use JSON templates as lightweight contracts between (micro)services. Use HTTPS with circuit breakers for synchronous communication. Use Redis or RabbitMQ for asynchronous communication. If your code can't get to Redis/RabbitMQ/another HTTP endpoint - die quickly rather than tying up resources.

###Lightweight data

Start with JSON in Redis. Move to JSON in MongoDB when you need to query the data with more flexibility. Place your BLOBs in AWS S3. Once you know whether your data - per (micro)service - needs to be consistent or available you can change data store as required. Cassandra is a great available data store. Postgres is a great consistent data store (if you can't afford Oracle RAC, which you can't). If you're generating huge quantities of events throw them into Hadoop.
  
###[Mutable state is the enemy](http://blog.hatofmonkeys.com/blog/2015/01/01/mutable-state/)

Generate events - immutable statements of fact - based upon actions. Simple, immutable, repeatable JSON events are a great start. [Store the events in an event log](http://martinfowler.com/eaaDev/EventSourcing.html) and use them to mutate the data stores powering consuming services - [separating commands from queries](http://martinfowler.com/bliki/CQRS.html).

###Customise Cloud Foundry when you need to

Customising Cloud Foundry is remarkably easy; do it when requirements demand. Adding buildpacks, services, even stacks ([I added Docker](http://www.cloudcredo.com/decker-docker-cloud-foundry/)) is straightforward. Don't start with Cloud Foundry customisation but don't be afraid to take the step if you need to. Deploy to your own IaaS or even your own metal if security/regulation/performance concerns necessitate it.

###Go fast and fail faster

In summary: get fast feedback about the software you're bringing to life. Fail fast if you're doing the wrong thing. Don't over-engineer; do what works, deliver quickly. Realise the opportunity cost of your (and your team's) time. Could you be building something more valuable instead?

[Christmas Garage! This one's relatively recent. And good.](https://www.youtube.com/watch?v=W_vM8ePGuRM)