---
layout: post
status: publish
published: true
title: tsuru server 1.1.0 is out!
author:
  display_name: Andrews Medina
  url: https://github.com/andrewsmedina
date: '2016-09-19 15:05:00 -0300'
date_gmt: '2016-09-19 18:05:00'
categories:
- Release
tags:
- release
comments: []
---

tsuru server 1.1.0, along with [tsuru client 1.1.0](https://github.com/tsuru/tsuru-client/releases/tag/1.1.0) has been released last week!

This release includes some awesome features and fixes. Please refer to the [release notes](http://docs.tsuru.io/en/stable/releases/tsurud/1.1.0.html) for the full list of features.

Some features worth highlighting are listed below:

* New event track system. Now all actions executed by users and by tsuru
itself are tracked [#1424](https://github.com/tsuru/tsuru/issues/1424).

* Support for cancelable events, right now, only the deploy event is cancelable. This means users can use the `tsuru event-cancel` command to ask for the cancelation of a deploy. tsuru will do it’s best to try cancelling it.

Backward incompatible changes (action needed)
=============================================

* Due to the new event tracking system, simply installing the new version of `tsurud` will cause deploy list and healing list to be empty. Running `tsurud migrate` will fix this by migrating deploys and healings to the new event system.

Grab it today!
==============

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/stable/installing/api.html#adding-repositories) or
building it from source.
