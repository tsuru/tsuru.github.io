---
layout: post
status: publish
published: false
title: tsuru easier to test (spoiler: packer is awesome).
author:
  display_name: Tarsis Azevedo
  url: https://github.com/tarsisazevedo
date: '2015-08-11 14:30:00 -0300'
date_gmt: '2015-08-11 14:30:00'
categories:
- Images
tags:
- images packer
comments: []
---

One of our goals this year is make tsuru easy to people who wants to try it for
the first time. To do it we are creating all-in-one aws and virtualbox vagrant
box images of tsuru with [packer](https://packer.io). These images are based on
stable and nightly packages.

## packer + tsuru now

Tsuru all-in-one images are builded as amazon ami and as vagrant virtualbox
box. These images are generated with [tsuru-now script](https://github.com/tsuru/now) and have the python platform installed by
default. The deploy method is pre-receive using archive server.

Amazon amis are builded in **us-east-1 region** and you can find it in
community amis as tsuru-stable or tsuru-nightly,
or get the latest ami id for [stable](https://s3.amazonaws.com/tsuru-images/nightly-ami-id) and [nightly](https://s3.amazonaws.com/tsuru-images/nightly-ami-id) here. 

Vagrant box can be founded in:

> [stable box](https://s3.amazonaws.com/tsuru-images/tsuru-stable-virtualbox.box)

> [nightly box](https://s3.amazonaws.com/tsuru-images/tsuru-nightly-virtualbox.box)


If you want to build these images by yourself, you can get our [conf files here](https://github.com/tsuru/tsuru-packer).
After checking out the repository you have to run: 

> $ make setup

> $ AWS_ACCESS_KEY=<your-access-key> AWS_SECRET_KEY=<your-secret-key> packer build tsuru-{nightly,stable}.json

With this we want to make the first contact with tsuru easier and attract more
people to project.

Thanks!
