---
layout: post
status: publish
published: true
title: tsuru server 0.9.0 is out!
author:
  display_name: Andrews Medina
  email: andrewsmedina@gmail.com
  url: http://andrewsmedina.com
date: '2014-12-02 18:30:00 -0200'
date_gmt: '2014-12-02 20:30:00'
categories:
- Release
tags:
- release
---

tsuru server 0.9.0 is out!

The main feature of this release is the experimental support to auto scale applications.

##Other features worth highlighting:

* API key that enable authentication without interaction. The can be regenerated using the command tsuru token-regenerate. To view the current key just use the command tsuru token-show.
* templates to create machines in the IaaS provider with docker-node-add. See machine-template-add command for more details.
* TSURU_SERVICES environment variable: this environment variable lists all service instances that the application is bound. This enables binding an application to multiple instances of a service For more details, check the TSURU_SERVICES documentation.
* Improvements to EC2 IaaS provider, it now accepts user-data config through iaas:ec2:user-data and a timeout for machine creation with iaas:ec2:wait-timeout config.
* A new debug route is available in the API: /debug/goroutines. It can only be hit with admin credentials and will dump a trace of each running goroutine.

##Backward incompatible changes

* Service API flow: the service API flow has changed, splitting the bind process in two steps: binding/unbinding the application and binding/unbinding the units. The old flow is now deprecated

You can see the complete list of features in the [release notes of tsuru server 0.9.0](http://docs.tsuru.io/en/0.9.0/releases/tsr/0.9.0.html).

Grab it today!

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/0.9.0/installing/api.html#adding-repositories) or building it from source.
