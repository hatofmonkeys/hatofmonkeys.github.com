---
layout: post
title: "Configuration Management isn't Stupid, but it Should Be"
date: 2014-03-15 10:37
comments: true
categories: 
---
Devops is about holistic, systems-orientated thinking; it's been misappropriated to be about configuration management. I've noticed a decline in the number of people from a development background at Devops conferences - maybe they've lost interest in talking about Puppet vs Chef vs Salt vs Ansible vs CFEngine vs X vs Y vs Z?

###Bricks
The role of infrastructure should be to provide reliable, consumable bricks to enable innovation at higher levels. If we create beautiful, unique, novel bricks it becomes impossible to build houses. This is a problem I see regularly with OpenStack deployments; they're amazing, wonderful, unique, organic. I cannot, however, easily deploy platforms to them.

###Configuration Management
This issue manifests itself in deployments orchestrated by configuration management.

- Complexity - you can do some amazing things in Chef as you have the power and flexibility to run arbitrary Ruby during your deployments. I have seen this abused many times - and done this myself. Too much clever branching logic and too little reliable code
- Determinism - configuration management tools often provide a thin veneer over non-deterministic operating system commands
- Reproducibility - server scaling operations often fail due to poor dependency management and non-deterministic actions

Configuration management is too focused on innovation at the server level rather than thinking about the entire system. Devops has become a silo.

###A Better Way
There are some tools and patterns emerging to tackle these problems.

- [Immutable infrastructure](http://foodfightshow.org/2013/07/immutable-infrastructure.html) - remove the drift
- [Docker](https://www.docker.io/)/[Decker](https://www.youtube.com/watch?v=QslNszh3jfY) - testable, simple, small, disposable containers
- [Nix](http://nixos.org/nix/) - declarative, deterministic package management
- [OSV](https://github.com/cloudius-systems/osv) - stupid(brilliant) operating system to enable innovation
- [BOSH](http://bosh.cfapps.io/) - stupid(brilliant) tool to deploy complex distributed systems
- [Mesos](http://mesos.apache.org/) - schedule commands(jobs) to run in a distributed environment
  
###'Infrastructure as Code' to 'Infrastructure as Good Code'
We need [SOLID](http://www.codeproject.com/Articles/60845/The-S-O-L-I-D-Object-Oriented-Programming-OOP-Prin) for infrastructure. We need to develop standardised, commoditised, loosely coupled, single-responsibility components from which we can build higher-order systems and services. Only then will we be enabling innovation higher up the value chain.

Devops should be about enabling the business to deliver effectively. We've got stuck up our own <del>arses</del> configuration management.
