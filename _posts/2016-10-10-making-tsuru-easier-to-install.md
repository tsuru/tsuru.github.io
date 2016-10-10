---
layout: post
status: publish
published: true
title: Making tsuru easier to install on any cloud
author:
  display_name: André Carvalho
  url: https://github.com/andrestc
date: '2016-10-10 15:05:00 -0300'
date_gmt: '2016-10-10 18:05:00'
categories:
- Features
tags:
- Docker Machine
- Swarm
- Docker
comments: []
---

tsuru client 1.1.1 comes with a experimental feature called **tsuru installer**. With tsuru installer
it is easy to start a new tsuru installation, including a multi-node installation. It's an great
way to try tsuru out, both on a local machine or in a multi-node installation on the cloud.

To install tsuru locally(in a VirtualBox VM), just run:

`tsuru install`

It's possible to use the installer to provision an entire multi-node infrastructure to run tsuru on a
large set of IaaS, like EC2, Azure, GCE etc. For more information, check the [documentation](https://docs.tsuru.io/stable/experimental/installer.html).

How it works
------------

tsuru installer leverages [**Docker Machine**](https://docs.docker.com/machine/) to create Docker hosts and that is what makes it able to provision hosts on a large set of IaaS and also makes it extensible: if your IaaS is not supported by Docker Machine, it is easy to develop an driver to do the heavy lifting.

On a multi-node installation, the installer provision and manages two kinds of hosts: core hosts and apps hosts. You can control how many of each you want on your installation.

Core hosts are Swarm nodes and are responsible for running tsuru core components as swarm services (orchestrated by Swarm). All this nodes are part of a Swarm cluster running on the newly launched [Swarm Mode](https://docs.docker.com/engine/swarm/) (released on Docker 1.12).

Apps hosts are Docker hosts registered as Docker nodes on tsuru. These are responsible for running tsuru apps (orchestrated by tsuru).

The future
----------

It's important to mention that this feature is currently experimental and is not ready for production use.

Our main goal is to make it easy to install a **production ready** tsuru. There are many challenges ahead but we think we are on the right way to do it. We have a [list of issues](https://github.com/tsuru/tsuru/issues?q=is%3Aissue+is%3Aopen+label%3Ainstaller) to address before recommending it for production use, these include making it possible to scale each component, making it possible to manage your installation (adding/removing nodes, updating the components etc) and leverage more of the services each IaaS provides (like load balancers and object storages, for example).

We are really looking forward to have feedback on the installer, don't hesitate to talk to us on [Gitter](https://gitter.im/tsuru/tsuru) or by filling an [issue on github](https://github.com/tsuru/tsuru/issues).
