---
layout: post
status: publish
published: true
title: tsuru server 0.11.0 is out!
author:
  display_name: Francisco Souza
  url: https://github.com/fsouza
date: '2015-05-07 16:00:00 -0300'
date_gmt: '2015-05-07 13:00:00'
categories:
- Release
tags:
- release
comments: []
---

tsuru server 0.11.0, along with [tsuru client 0.16.0](https://github.com/tsuru/tsuru-client/releases/tag/0.16.0) and [tsuru-admin 0.10.0](https://github.com/tsuru/tsuru-admin/releases/tag/0.10.0), is out today!

This release includes some awesome features and fixes. Please refer to the [release notes](http://docs.tsuru.io/en/stable/releases/tsr/0.11.0.html) for the full list of features.

Some features worth highlighting are listed below:

* Pool management overhaul. Now pools are a concept independent on the Docker provisioner. Users can now have multiple pools associated with each team. If that’s the case, when creating a new application, users will be able to choose which pool they want to use to deploy it;
* Node auto scaling. It’s now possible to enable automatic scaling of Docker nodes, this will add or remove nodes according to rules specified in your tsuru.conf file. There's a dedicated page in our documentation for [node autoscaling](http://docs.tsuru.io/en/stable/advanced_topics/node_scaling.html).

Backward incompatible changes
=============================

* There are two migrations that must run before deploying applications with tsr 0.11.0, they concern pools and can be run with tsr migrate. The way pools are handled has changed. Now it’s possible for a team to have access to more than one pool, if that’s the case the pool name will have to be specified during application creation;
* Queue configuration is necessary for creating and removing machines using a IaaS provider. This can be simply done by indicating a MongoDB database configuration that will be used by tsuru for managing the queue. No external process is necessary. See [configuration reference](http://docs.tsuru.io/en/stable/reference/config.html#config-queue) for more details;
* Previously it was possible for more than one machine have the same address this could cause a number of inconsistencies when trying to remove said machine using ``tsuru docker-node-remove --destroy``. To solve this problem tsuru will now raise an error if the IaaS provider return the same address of an already registered machine.

Contributors
============

Besides the core team, this release was also powered by external contributors.  And we want to thank them for helping getting tsuru server 0.11.0 out. Here is the list of contributors that helped in this version:

- Anna Shipman
- Diogo Munaro Vieira
- Felippe da Motta Raposo
- Gustavo Pantuza
- Lucas Weiblen
- Marc Abramowitz
- Martin Jackson
- Pablo Aguiar
- Samuel ROZE
- Wilson Júnior

Grab it today!
==============

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/stable/installing/api.html#adding-repositories) or building it from source.
