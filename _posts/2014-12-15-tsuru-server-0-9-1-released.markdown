---
layout: post
status: publish
published: true
title: tsuru server 0.9.1 is out!
author:
  display_name: Andrews Medina
  email: andrewsmedina@gmail.com
  url: http://andrewsmedina.com
date: '2014-12-15 18:30:00 -0200'
date_gmt: '2014-12-05 20:30:00'
categories:
- Release
tags:
- release
---

In the 0.9.0 and 0.9.1 a lot of features are added. The features that worth highlighting are:

* The experimental support to auto scale applications. If you are using the metric system with Statsd/Graphite it is possible scale the number of the units for your application automatically. We will create a dedicated blog post about this feature in the future.
* API key that enables authentication without interaction. The key can be regenerated using the command `tsuru token-regenerate`. To view the current key just use the command `tsuru token-show`. You can see more information about the new commands in the [client reference](http://docs.tsuru.io/en/master/reference/tsuru-client.html#authentication).
* templates to create machines in the IaaS provider with docker-node-add. [See machine-template-add command for more details](http://docs.tsuru.io/en/master/reference/tsuru-admin.html#tsuru-admin-machine-template-add-cmd).
* TSURU_SERVICES environment variable: this environment variable lists all service instances that the application is bound. This enables binding an application to multiple instances of a service. [For more details, check the TSURU_SERVICES documentation](http://docs.tsuru.io/en/master/services/tsuru-services-env-var.html).
* Improvements to EC2 IaaS provider, it now accepts user-data config through iaas:ec2:user-data and a timeout for machine creation with iaas:ec2:wait-timeout config.
* A new debug route is available in the API: /debug/goroutines. It can only be hit with admin credentials and will dump a trace of each running goroutine.
* The [unit flow](http://docs.tsuru.io/en/master/using/unit-states.html) was changed to use correct status on build. The unused status (unreachable and down) was removed. And `Created` status was added. Now the unit flow is:

```
+----------+                           Start          +---------+
| Building |                   +---------------------+| Stopped |
+----------+                   |                      +---------+
      ^                        |                           ^
      |                        |                           |
 deploy unit                   |                         Stop
      |                        |                           |
      +                        v       RegisterUnit        +
 +---------+  app unit   +----------+  SetUnitStatus  +---------+
 | Created | +---------> | Starting | +-------------> | Started |
 +---------+             +----------+                 +---------+
                               +                         ^ +
                               |                         | |
                         SetUnitStatus                   | |
                               |                         | |
                               v                         | |
                           +-------+     SetUnitStatus   | |
                           | Error | +-------------------+ |
                           +-------+ <---------------------+
```

Backward incompatible changes
=============================

* Service API flow: the service API flow has changed, splitting the bind process in two steps: binding/unbinding the application and binding/unbinding the units. The old flow is now deprecated

You can see the complete list of features in the release notes of tsuru server [0.9.0](http://docs.tsuru.io/en/master/releases/tsr/0.9.0.html) and [0.9.1](http://docs.tsuru.io/en/master/releases/tsr/0.9.1.html).

Grab it today!
==============

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/master/installing/api.html#adding-repositories) or building it from source.
