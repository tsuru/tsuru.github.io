---
layout: post
status: publish
published: true
title: Using Packer to speed-up your first experience with tsuru
author:
  display_name: Tarsis Azevedo
  url: https://github.com/tarsisazevedo
date: '2015-09-02 18:30:00 -0300'
date_gmt: '2015-09-02 21:30:00'
categories:
- Images
tags:
- images packer
comments: []
---

If you have ever used [tsuru-bootstrap](https://github.com/tsuru/tsuru-bootstrap) before, you know how slow it can get. If you have never used it, you should know that running a command and then waiting 30 minutes to get tsuru up and running is not ideal. What if we could do it in 2 minutes? Time to get faster!

In order to achieve this goal, we are creating all-in-one AWS and VirtualBox vagrant box images of tsuru with [Packer](https://packer.io). These images are based on stable and nightly releases.

## Packer + tsuru now

Tsuru all-in-one images are built as Amazon AMI and as Vagrant VirtualBox box. We're using [tsuru-now](https://github.com/tsuru/now) to build the images. They come bundled with the Python platform, and with tsuru configured to use the pre-receive hook on top of [archive-server](https://github.com/tsuru/archive-server).

Amazon AMIs are available in **us-east-1 region** and you can find it in "Community AMIs" tab when launching a new instance. It's also possible to get the latest AMIs programmatically by downloading two files from S3:

    $ curl https://s3.amazonaws.com/tsuru-images/nightly-ami-id
    ami-1350d678

    $ curl https://s3.amazonaws.com/tsuru-images/stable-ami-id
    ami-a98527c2

There are Vagrant boxes for the VirtualBox provider as well. They come in the same two flavors as the ones provided in EC2: stable and nightly.

The URLs for boxes are listed bellow:

* stable: [https://s3.amazonaws.com/tsuru-images/tsuru-stable-virtualbox.box](https://s3.amazonaws.com/tsuru-images/tsuru-stable-virtualbox.box)
* nightly: [https://s3.amazonaws.com/tsuru-images/tsuru-nightly-virtualbox.box](https://s3.amazonaws.com/tsuru-images/tsuru-nightly-virtualbox.box)

Users may write the URL directly in the Vagrantfile, or use it in the ``vagrant init``:

    $ vagrant init tsuru-stable https://s3.amazonaws.com/tsuru-images/tsuru-stable-virtualbox.box

    $ vagrant init tsuru-nightly https://s3.amazonaws.com/tsuru-images/tsuru-nightly-virtualbox.box


## building the images

If you want to build these images yourself, you can get our [conf files here](https://github.com/tsuru/tsuru-packer). After checking out the repository you have to run:

    $ make setup

    $ AWS_ACCESS_KEY=<your-access-key> AWS_SECRET_KEY=<your-secret-key> packer build tsuru-{nightly,stable}.json

If you want to talk more about this project or any other [tsuru-related project](https://github.com/tsuru) feel free to reach us by openning an issue in [our Github repository](https://github.com/tsuru/tsuru/issues), directly chatting in our [Gitter room](https://gitter.im/tsuru/tsuru) or posting a message to the [tsuru-users group](https://groups.google.com/forum/#!forum/tsuru-users).
