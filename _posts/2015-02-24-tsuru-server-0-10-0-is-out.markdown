---
layout: post
status: publish
published: true
title: tsuru server 0.10.0 is out!
author:
  display_name: Francisco Souza
  login: francisco
  email: fss@corp.globo.com
  url: http://f.souza.cc
author_login: francisco
author_email: fss@corp.globo.com
author_url: http://f.souza.cc
date: '2015-02-24 10:00:00 -0300'
date_gmt: '2015-02-24 13:00:00'
categories:
- Release
tags:
- release
comments: []
---

tsuru server 0.10.0, along with [tsuru client 0.15.0](https://github.com/tsuru/tsuru-client/releases/tag/0.15.0) and [tsuru-admin 0.9.0](https://github.com/tsuru/tsuru-admin/releases/tag/0.9.0), is out today!

This release includes some awesome features and fixes. Please refer to the [release notes](http://docs.tsuru.io/en/latest/releases/tsr/0.10.0.html) for the full list of features. In order to take advantage of the new features, please make sure that you have the latest version of tsuru's components, specially Docker (at least version 1.4, check the [upgrading Docker page](http://docs.tsuru.io/en/latest/managing/upgrading-docker.html) for proper instructions in the upgrading process) and Gandalf (at least version 0.6.0).

Some features worth highlighting are listed below:

* [Gandalf](https://github.com/tsuru/gandalf) is now optional. When Gandalf is not configured, users will be able to deploy code only using ``app-deploy``. In order to use ``git push`` deployment, Gandalf must be enabled and configured. Please refer to the [managing Git repositories and keys](http://docs.tsuru.io/en/latest/managing/repositories.html) for more details;
* tsuru now support rollbacks! It will store multiple image versions of an application (one for each deployment) and allow the user to roll back to a specific version. For more details, check the [app-deploy-rollback command](http://tsuru-client.readthedocs.org/en/latest/reference.html#rollback-deploy);
* tsuru now has an improved healthcheck that allow users to better diagnostic failures in the server. Sending a request to the URL ``/healthcheck?check=all`` will print the status of components in tsuru, including EC2, CloudStack, Gandalf, MongoDB and Docker. For more details, see [issue #967](https://github.com/tsuru/tsuru/issues/967);
* more powerful flexible platforms: the new [PHP](https://github.com/tsuru/basebuilder/tree/master/php) and [Ruby](https://github.com/tsuru/basebuilder/tree/master/ruby) platforms are more flexible now and are configurable, like in the [Java platform](https://github.com/tsuru/basebuilder/tree/master/java)
  - Thanks to Samuel ROZE, the PHP platform support multiple interpretors (FPM and mod_php) and frontends (Apache or nginx).
  - The Ruby platform supports switching between Ruby versions by specifying the desired version in the ``Gemfile`` or ``.ruby-version`` file.

##Backward incompatible changes

* Drop support for Docker images that do not run [tsuru-unit-agent](https://github.com/tsuru/tsuru-unit-agent). Starting on tsuru-server 0.10.0, tsuru-unit-agent is no longer optional.

##Contributors

Besides the core team, this release was also powered by external contributors.  And we want to thank them for helping getting tsuru server 0.10.0 out. Here is the list of contributors that helped in this version:

* Alessandro Corbelli
* Lucas Weiblen
* Marc Abramowitz
* Mateus Del Bianco
* Rogério Yokomizo
* Samuel ROZE

##Grab it today!

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/latest/installing/api.html#adding-repositories) or building it from source.
