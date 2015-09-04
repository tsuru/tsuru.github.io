---
layout: post
status: publish
published: true
title: tsuru server 0.12.2 is out!
author:
  display_name: Francisco Souza
  url: https://github.com/fsouza
date: '2015-09-04 11:56:00 -0300'
date_gmt: '2015-09-04 14:56:00'
categories:
- Release
tags:
- release
comments: []
---

tsuru server 0.12.2, along with [tsuru client 0.17.1](https://github.com/tsuru/tsuru-client/releases/tag/0.17.1) and [tsuru-admin 0.11.0](https://github.com/tsuru/tsuru-admin/releases/tag/0.11.0), has been released this week!

This release includes some awesome features and fixes. Please refer to the [release notes](http://docs.tsuru.io/en/stable/releases/tsurud/0.12.2.html) for the full list of features.

Some features worth highlighting are listed below:

* Lean containers: this is definitely the big feature of this release. With lean containers, we've dropped Circus, making application images smaller, and containers faster. Improving resource usage, because application containers won't run [tsuru-unit-agent](https://github.com/tsuru/tsuru-unit-agent/) anymore either. It's still used during the deployment process, but it's not competing with the application process anymore.
* Pool management improvements. There are now three kinds of pools:
  - team pools: these pools are segregated by teams, and cloud administrators can associate teams to pools. When creating an application, this pool must be chosen explicitly
  - public pools: these pools are available to all teams, and must be chosen explicitly as well
  - default pool: this is a single pool that replaced the old fall back pool. It's the implicit pool used for applications when no pool is specified
* New router available: [Vulcand](https://vulcand.io). Vulcand is a powerful reverse proxy, with SNI based TLS support. This is the first step on being able to configure TLS on applications (see [issue #1206](https://github.com/tsuru/tsuru/issues/1206)).

Backward incompatible changes
=============================

* As this version creates containers per processes, whenever an application has more than one process, tsuru will forward requests to the process named "web". So, in a Procfile like the one below, "api" should be replaced with "web":

```
api: ./start-api
worker1: ./start-worker1
worker2: ./start-worker2
```

* tsr has been renamed to tsurud. Please update any procedures and work flows (including upstart and other init scripts).
* The fallback pool should be changed to default pool. Doing that is as simple
  as running the command ``tsuru-admin pool-update pool_name --default=true``

A new release policy
====================

As you have might noticed, we released tsurud 0.12.0 on August 27th, then released 0.12.1 on September 2nd, and then released 0.12.2 on September 3rd. This is definitely not a good way of managing releases.

We already have a flow for constant testing on nightly packages, ensuring that everything works, but this testing doesn't reach a good scale yet. As we work to improve this flow, we're also committing to provide more stable releases, by defining a clearer release cycle:

Whenever we reach the stable stage of development, we're going to provide a release candidate (rc) package, and run the rc version on our production environment. If we caught any bad behavior, we fix it and issue another rc version. After some days of running the rc release, as soon as we feel comfortable about it (one week later, possible), a new release will be tagged and safely advised as stable by the tsuru core team.

Contributors
============

Besides the core team, this release was also powered by external contributors. And we want to thank them for helping getting tsuru server 0.12.2 out. Here is the list of contributors that helped in this version:

- Dan Carley
- Dan Hilton
- Jonathan Prates
- Leandro Souza
- Richard Knop

Grab it today!
==============

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/stable/installing/api.html#adding-repositories) or building it from source.
