---
layout: post
status: publish
published: true
title: tsuru server 0.10.1 is out
author:
  display_name: Francisco Souza
  login: francisco
  email: fss@corp.globo.com
  url: http://f.souza.cc
author_login: francisco
author_email: fss@corp.globo.com
author_url: http://f.souza.cc
date: '2015-02-26 18:37:00 -0300'
date_gmt: '2015-02-26 15:37:00'
categories:
- Release
tags:
- release
comments: []
---


Today we're releasing [tsuru-server 0.10.1](http://docs.tsuru.io/en/latest/releases/tsr/0.10.1.html), two days after the 0.10.0 release, to fix some potential bugs:

* In the last release, we changed the way tsuru names Docker images, and the API daemon included an automatic migration routine that run during start-up. We expected this routine to slow down only the **first** start-up, after upgrading. But it ends up slowing down every startup. In order to fix this issue, we ensure that the migration routine do not try to migrate applications that are already migrated;
* There was an old issue with the healing of Docker nodes: tsuru detects and tracks failures when interacting with Docker, and after some configurable threshold, the API triggers the healing (replacing the nodes). The 0.10.1 release reduced the probability of false positives in failure detection, by properly handling image failures in Docker;
* Fixed a security flaw in the tsuru API that allowed users to deploy code to apps that they do not have access.

We apologize for any incoveniences that these issues may have caused to our users. As usual, you can upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/latest/installing/api.html#adding-repositories) or building it from source.
