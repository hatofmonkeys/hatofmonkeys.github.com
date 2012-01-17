---
layout: post
title: "System Build Reproducibility"
date: 2012-01-15 09:59
comments: true
categories: 
---
I've been on the receiving end of build reproducibility rants from [developers](http://www.freakingnews.com/pictures/34500/Cyclops-Teletubbies-34621.jpg) at plenty of conferences. Their bile is usually aimed at [Maven's snapshot functionality](http://maven.apache.org/general.html#snapshot-artifacts). I've often questioned how reproducible their systems are; I'm usually met by a blank look.

I've always aimed to make system builds reproducible, but with little success. Gem, pear, pecl, rpm, license agreements, configure/make/make install: they all take their toll. This can lead to inconsistent builds between environments - or even in a single tier - due to scaling up/down.

As I've tended to use RPM-based systems ([misspent youth](http://www.redhat.com/certification/rhca/)), I've attempted, wherever possible, to get all non-configuration files on a server into RPMs. I've been more promiscuous with configuration management, moving from home grown, to [Cfengine](http://cfengine.com/), via [Puppet](http://puppetlabs.com/), to [Chef](http://www.opscode.com/chef/). I'm currently using chef-solo, with tooling such as [Noah](https://github.com/lusis/Noah) and [MCollective](http://puppetlabs.com/mcollective/) for orchestration. Don't even mention the number of deployment/ALM tooling solutions I've been through(although [Capistrano](https://github.com/capistrano/capistrano/wiki) has never annoyed me to any great extent).

Even with long term usage of RPMs, build reproducibility has been far from simple. [RH Satellite](http://www.redhat.com/red_hat_network/)/[Spacewalk](http://spacewalk.redhat.com/) should make this easy, but unfortunately it's a bloated mess. I've usually resorted to simple apache/createrepo, but this poses its own problems. Do you have a repo per environment? How do you track which servers were built against which repo? How do you roll out updates in a manageable fashion?

I've created a simple setup called [Yumtags\!](https://github.com/hatofmonkeys/yumtags) to address some of these issues. The basic idea is that you can drop RPMs in to a directory, and then "freeze" the directory at that point in time by creating and storing repository metadata against a tag. This tag can then be used, perhaps in a chef-solo-driven repository definition, to update, build, and reproduce systems in a known state. It currently features simple JSON-driven integration for CI systems, so RPM-based integration pipelines can be easily automated. There's a million and one things missing from it, but now it does the basic story I've shared it for others to hack on.