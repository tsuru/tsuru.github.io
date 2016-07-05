---
layout: post
status: publish
published: true
title: tsuru server 1.0.0 is out!
author:
  display_name: Andrews Medina
  url: https://github.com/andrewsmedina
date: '2016-07-04 16:08:00 -0300'
date_gmt: '2016-07-04 19:08:00'
categories:
- Release
tags:
- release
comments: []
---

tsuru server 1.0.0, along with [tsuru client 1.0.1](https://github.com/tsuru/tsuru-client/releases/tag/1.0.1) and [tsuru-admin 1.0.0](https://github.com/tsuru/tsuru-admin/releases/tag/1.0.0), has been released last week!

This release includes some awesome features and fixes. Please refer to the [release notes](http://docs.tsuru.io/en/stable/releases/tsurud/1.0.0.html) for the full list of features.

Some features worth highlighting are listed below:

* Deploy applications using Docker image
([#1314](https://github.com/tsuru/tsuru/issues/1314)). Now it’s possible to deploy
a Docker image as tsuru app using tsuru app-deploy -i command. This image should
be in a registry and be accessible by tsuru api. Image should also have a
`Entrypoint` or a `Procfile` at given paths, `/` or `/app/user/` or
`/home/application/current`. See more in [tsuru-client app-deploy reference](https://tsuru-client.readthedocs.io/en/latest/reference.html#deploy).

* Improved application log handling. Besides several performance improvements in
log handling, it’s now possible to configure tsuru to forward containers logs
directly to an external log server. Please check [Managing Application Logs](https://docs.tsuru.io/master/managing/logs.html) for more details.

* API versioning. Now all API calls to tsuru may include a version prefix in the
format `/1.0/<request path>`. Further changes to the API will be versioned
accordingly.

* EC2 IaaS is now feature complete, supporting parameter such as IAM roles, extra volumes and multiple network interfaces. Since these parameters are composed of multiple values, users must provide a JSON for using them. It also supports using private DNS names now, as long as the user specifies the subnet-id and the index of the network interface that they want to use. For example, with IAM instance profiles, block devices and running on a private network:

```
$ tsuru-admin docker-node-add iaas=ec2 'iaminstanceprofile={"name":"docker-instances"}' 'blockdevicemappings=[[{"DeviceName":"/dev/sda1","Ebs":{"VolumeSize":100}}]' subnetid=subnet-1234 network-index=0 ...
```

* New SAML V2 authentication scheme. See SAML authentication configuration for
instructions on how to configure it.

Backward incompatible changes (action needed)
=============================================

* The way the `bs` container is managed has changed. If you have any
configuration setting for `bs` that was added using `tsuru-admin bs-env-set`
you must run `tsurud migrate` to ensure every config env has been copied to
the new structure.

`bs` containers should now be managed using
`tsuru-admin node-container-update big-sibling [options...]`. See
[node containers reference](https://tsuru-admin.readthedocs.io/en/master/reference.html#node-containers-management) for more information.

Contributors
============

Besides the core team, this release was also powered by external contributors.
And we want to thank them for helping getting tsuru server 1.0.0 out. Here is
the list of contributors that helped in this version:

- Diego Araujo and USP
- James Pic
- Paulo Alem
- Pedro Medeiros
- Piotr Komborski
- Renan Mendes Carvalho
- Rodrigo Oliveira

Grab it today!
==============

You can install or upgrade tsuru server using our [PPA](http://docs.tsuru.io/en/stable/installing/api.html#adding-repositories) or
building it from source.
