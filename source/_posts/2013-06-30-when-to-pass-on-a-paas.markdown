---
layout: post
title: "When to Pass on a PaaS"
date: 2013-06-30 18:04
comments: true
categories: 
---
There's no point pretending I don't love 'The PaaS'. I do. I have spent too much of my career fighting battles I shouldn't be fighting; re-inventing similar-looking systems time and time again. The idea I could just drop an application into a flexible platform and expect it to run, without consuming my entire life for the preceeding three months writing Chef cookbooks and wrestling EC2, sounds fantastic.

### Cloud Foundry

Having played with Heroku, and being dismayed at not being able to play with my own Heroku, I was overjoyed when VMWare released Cloud Foundry. I created a Vagrant box on the Cloud Foundry release day and began distributing it to clients. I worked with one of my clients at the time, OpenCredo, to develop and deploy one of their new services to a Cloud Foundry installation I created. I believe this was the first SLA-led production deployment of Cloud Foundry globally.

I spoke about the rationale behind running/developing your own PaaS at QCon London 2012. I also discussed some of the use cases I'd fulfilled using PaaS, including OpenCredo's.

[QCon 2012 - Lessons Learned Deploying PaaS](http://www.infoq.com/presentations/Lessons-Learned-in-Deploying-PaaS)

### OpenShift

I was similarly happy when I heard RedHat had bought Makara, a product I'd briefly experimented with, and were looking at producing their own PaaS. I've used RedHat-based systems for many years with great success, have always found [YUM/RPM great to use](/blog/2012/01/15/system-build-reproducibility/), and was apparently the 7th person in the UK to achieve RedHat Architect status. A RedHat-delivered PaaS would surely be the panacea for all my problems.

I was scoping a large project at this time with availability as a prime concern. It occurred to me that I could use two turnkey PaaSes simultaneously, Cloud Foundry and OpenShift, such that if there was an issue with either I could simply direct all traffic to the other PaaS. I discussed the deployment and progress at DevopsDays.

[DevopsDays Rome 2012 - How I Learned to Stop Worrying and Love the PaaS](http://new.livestream.com/devopsdaysorg/devopsdaysRome/videos/4516372) - I start about 32 minutes in.

### From Dream to Reality

Unfortunately, the project didn't quite work out as planned. We had a number of issues with OpenShift which meant we had no choice but to withdraw it from production usage. Scalability was an enormous problem; bringing an application to production scale was a sub-twenty second operation in Cloud Foundry; it took fourty-eight hours plus in OpenShift. We had to write our own deployment and orchestration layer for OpenShift based on Chef and shell - Cloud Foundry has the fantastic BOSH tool enabling deployment, scaling, and upgrades. These reasons, alongside some nasty bugs and outages, meant we were unable to use OpenShift for our deployment.

Beyond this I feel OpenShift, like many 'PaaSish' systems, has got the focus wrong. There seems to be a plethora of container-orchestration systems being produced at the moment, which are really just a slight re-focus on the IaaS abstraction layer. OpenShift is in danger of falling into this trap. PaaS needs to remain focussed on the application as the unit of currency, and not the container or virtual machine. It looks entirely possible (and would make an interesting project) to run Cloud Foundry inside OpenShift, illustrating the conceptual difference.

We settled on using distributed Cloud Foundry instances across diverse IaaS providers to deliver the project; it was a great success. I blogged about it for Cloud Foundry's blog.

[CloudFoundry.com blog post - UK Charity Raises Record Donations Powered by Cloud Foundry](http://blog.cloudfoundry.com/2013/04/30/uk-charity-raises-record-donations-powered-by-cloud-foundry/)

### Which PaaS?

I've remained supportive of RedHat's efforts to deliver a PaaS solution but fear they're not quite there yet. I organised a [London PaaS User Group meetup  to help RedHat to put their side of the case across to the London community](http://www.meetup.com/London-PaaS-User-Group-LOPUG/events/120336492/). It sounded like they had some exciting developments in the pipeline but even with the new features it's likely we would have been unable to deliver the enterprise-grade services our project required. 

Perhaps Redhat's customer base are largely systems administrators rather than developers. Perhaps Redhat have more experience at deploying and managing servers than applications. For whatever reason, I think it would be a denigration of PaaS to allow it to be misconstrued as container-based IaaS. Containers can be a by-product of service provision but should not be the focus of PaaS.

Cloud Foundry isn't perfect but, at the moment, is the only PaaS product I'd recommend to anyone looking to make a long-term investment.
