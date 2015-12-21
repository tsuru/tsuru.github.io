---
layout: post
status: publish
published: true
title: tsuru server 0.13.0 is out!
author:
  display_name: Francisco Souza
  url: https://github.com/fsouza
date: '2015-12-21 16:08:00 -0200'
date_gmt: '2015-12-21 18:08:00'
categories:
- Release
tags:
- release
comments: []
---

tsuru server 0.13.0, along with [tsuru client 0.18.1](https://github.com/tsuru/tsuru-client/releases/tag/0.18.1) and [tsuru-admin 0.12.1](https://github.com/tsuru/tsuru-admin/releases/tag/0.12.1), has been released last week!

This release includes some awesome features and fixes. Please refer to the [release notes](http://docs.tsuru.io/en/stable/releases/tsurud/0.13.0.html) for the full list of features.

Some features worth highlighting are listed below:

* New authorization system: tsuru now supports more granular authorization system, with roles and permissions. Roles group permissions, and are associated with users.

* New IaaS available: tsuru now supports DigitalOcean, along with Amazon EC2 and CloudStack. Privileged users are able to spawn droplets on DigitalOcean and use them as managed nodes with tsuru.

* Platforms can now be enabled and disabled by privileged users. Disabled platforms can be used by privileged users, who can also upgrade the platform and enabled it back later, making it available to all users.

* New router: support new version of [Galeb](http://galeb.io), which is now fully open source. Galeb is a very fast router, written in Java, with WebSocket support. It was also born at Globo.com. Users from the community can now choose to use Galeb, along with [Vulcand](http://vulcand.io) and [Hipache](https://github.com/tsuru/planb).

Backward incompatible changes
=============================

* The new authorization system requires roles to be associated with permissions and users to be associated with roles. So after upgrading, users do not have any permissions, and roles and permissions must be created and associated with the user. There's an optional migration that can be used to keep tsuru compatible with the previous behavior. Please refer to the [migrating section in the Permissions documentation](http://docs.tsuru.io/en/stable/managing/users-and-permissions.html#migrating-perms).

* The post-receive hook is no longer supported, please use one of the available [pre-receive hooks](https://github.com/tsuru/tsuru/tree/master/misc/git-hooks).

* If you're using the [archive-server](https://github.com/tsuru/archive-server), we recommend upgrading it and also the [pre-receive hook](https://github.com/tsuru/tsuru/blob/master/misc/git-hooks/pre-receive.archive-server).

The new release process
=======================

Starting with this release, we're now running a new release process, that included 12 release candidates for tsurud 0.13.0. This means that we've been running tsuru 0.13.0 in production since November 6th, and as so we're well confident that this release is stable enough to be deployed in production by other companies using tsuru. So, feel safe to take this release to your production environment, and [please let us know](https://github.com/tsuru/tsuru/issues) if you find any issue on it!

Contributors
============

Besides the core team, this release was also powered by external contributors. And we want to thank them for helping getting tsuru server 0.13.0 out. Here is the list of contributors that helped in this version:

- Giuseppe Ciotta
- Guilherme Garnier
- Hugo Seixas Antunes
- Manoel Domingues Junior

Grab it today!
==============

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/stable/installing/api.html#adding-repositories) or building it from source.
