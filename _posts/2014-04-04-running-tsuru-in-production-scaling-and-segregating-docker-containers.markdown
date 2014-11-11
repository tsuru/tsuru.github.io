---
layout: post
status: publish
published: true
title: 'Running tsuru in production: scaling and segregating Docker containers'
author:
  display_name: Francisco Souza
  login: francisco
  email: fss@corp.globo.com
  url: http://f.souza.cc
author_login: francisco
author_email: fss@corp.globo.com
author_url: http://f.souza.cc
excerpt: tsuru is an open source PaaS, born in early 2012 at <a title="Globo.com"
  href="http://www.globo.com" target="_blank">Globo.com</a>, a brazilian media company.
  At a first moment, tsuru hit production using <a title="Juju" href="http://juju.ubuntu.com">Juju</a>
  to provision virtual machines on-demmand. Juju is an amazing tool, but provisioning
  virtual machines on-demmand is slow. Later, we started integrating with <a title="LXC"
  href="https://linuxcontainers.org/">Linux Containers (lxc)</a>, and <a title="Docker"
  href="http://docker.io">Docker</a> was born.
wordpress_id: 21
wordpress_url: http://blog.tsuru.io/?p=21
redirect_from:
  - /2014/04/04/running-tsuru-in-production-scaling-and-segregating-docker-containers/
date: '2014-04-04 17:49:23 -0300'
date_gmt: '2014-04-04 20:49:23 -0300'
categories:
- Architecture
tags:
- docker
- architecture
- docker cluster
- docker registry
comments:
- id: 2
  author: tsuru at OSCON 2014 | tsuru blog
  author_email: ''
  author_url: http://blog.tsuru.io/2014/04/11/tsuru-at-oscon-2014/
  date: '2014-04-11 17:16:09 -0300'
  date_gmt: '2014-04-11 20:16:09 -0300'
  content: "[&#8230;] We will cover each of these topics in future posts in this blog
    (there&#8217;s already a post about Docker in production). [&#8230;]"
- id: 4
  author: Akshi .mohan
  author_email: akshi200@gmail.com
  author_url: ''
  date: '2014-05-02 10:34:00 -0300'
  date_gmt: '2014-05-02 13:34:00 -0300'
  content: |-
    i needed help with deploying tsuru can anyone tell me where will I be able to contact ?? particular websie or email id??
    I have installed the server part !! what is the next step and is it right??
- id: 5
  author: Tarsis Azevedo
  author_email: tarsis.azevedo@gmail.com
  author_url: http://blog.tarsisazevedo.com/
  date: '2014-05-02 11:12:00 -0300'
  date_gmt: '2014-05-02 14:12:00 -0300'
  content: |-
    Hi Akshi,
    we have an IRC channel (#tsusu) in freenode and a general mailing list (https://groups.google.com/forum/?fromgroups#!forum/tsuru-users).
    You can see others informations on http://tsuru.io
- id: 11
  author: High-availability clusters | Niccolò Brogi
  author_email: ''
  author_url: http://www.nbrogi.com/2014/08/high-availability-cluster/
  date: '2014-08-10 13:42:14 -0300'
  date_gmt: '2014-08-10 16:42:14 -0300'
  content: "[&#8230;] http://blog.tsuru.io/2014/04/04/running-tsuru-in-production-scaling-and-segregating-docker-container&#8230;
    [&#8230;]"
- id: 15
  author: Diogo Goebel
  author_email: diogo.goebel@getupcloud.com
  author_url: https://getupcloud.com
  date: '2014-10-13 18:11:00 -0300'
  date_gmt: '2014-10-13 21:11:00 -0300'
  content: |-
    Hi, I have some questions :)
    How do you do the orchestration proccess? are you using kubernetes?
    Do we have isolation between docker containers in the same node? If yes, are you using SELinux or what else?


    cheers
- id: 16
  author: Francisco Souza
  author_email: f@souza.cc
  author_url: http://f.souza.cc
  date: '2014-10-13 18:25:00 -0300'
  date_gmt: '2014-10-13 21:25:00 -0300'
  content: |-
    Hi Diogo! tsuru does all the orchestration work, creating VMs using CloudStack or EC2 and running Docker container on them.


    Currently we don't have any network isolation between the containers in the same node. It's running just Docker, but we do plan to improve this setup in the future.


    Best,
    Francisco
---
<p>tsuru is an open source PaaS, born in early 2012 at <a title="Globo.com" href="http://www.globo.com" target="_blank">Globo.com</a>, a brazilian media company. At a first moment, tsuru hit production using <a title="Juju" href="http://juju.ubuntu.com">Juju</a> to provision virtual machines on-demmand. Juju is an amazing tool, but provisioning virtual machines on-demmand is slow. Later, we started integrating with <a title="LXC" href="https://linuxcontainers.org/">Linux Containers (lxc)</a>, and <a title="Docker" href="http://docker.io">Docker</a> was born.<a id="more"></a><a id="more-21"></a></p>
<p>Docker brought some light to our problems, and soon enough we started using it, abandoning our integration with lxc. After some months integrating with Docker, we were able to switch our production environment and start to scale it to run Docker on more than 20 hosts simultaneously. Docker and tsuru enabled Globo.com to run more than 1000 deployments in three months for some of its projects. But how does it work? How does the architecture look like?</p>
<p>There were two issues for running Docker in production: we needed to scale it; and make sure that we could isolate the applications that needed to be isolated. We need to be able to run containers across multiple Docker nodes and make sure that containers from some apps do not mess with resources from other applications.</p>
<p>The picture below presents the most important parts of tsuru's architecture related to Docker:</p>
<p><a href="http://tsurublog.s3.amazonaws.com/wp-content/uploads/2014/03/tsuru_arch1.png"><img class="alignnone  wp-image-23" alt="tsuru_arch(1)" src="http://tsurublog.s3.amazonaws.com/wp-content/uploads/2014/03/tsuru_arch1.png" width="637" height="634" /></a></p>
<p>In future posts, we will dig deeper in other components of this architecture. Let's focus now on Docker.</p>
<p>tsuru uses <a title="docker-cluster" href="https://github.com/tsuru/docker-cluster">docker-cluster</a> for distributing containers across multiple Docker nodes. A Docker node is simply a machine running the Docker daemon. docker-cluster is a Go package that enables Go programs to run Docker containers across clusters of Docker nodes. It contains an interesting component: the <a href="http://godoc.org/github.com/tsuru/docker-cluster/cluster#Scheduler">scheduler</a>. The scheduler is a Go interface, and users of the package are able to replace the default scheduler (that uses a round robin approach).</p>
<p>While docker-cluster by itself solves the issue of scaling, tsuru needed to provide an scheduler with the proper rules for segregating the containers of certain applications. And this is the segregated scheduler: it allocates a pool of Docker nodes to one or more teams.</p>
<p>Imagine there are 6 nodes in the cloud, and we want to split them between 3 teams: each team will get 2 nodes. There will be an association in tsuru:</p>
<pre><code>+-----------+--------------------------------+--------+
| Node name | Node host                      | Teams  |
+-----------+--------------------------------+--------+
| node01    | http://node01.company.com:4243 | team a |
| node02    | http://node02.company.com:4243 | team a |
| node03    | http://node03.company.com:4243 | team b |
| node04    | http://node04.company.com:4243 | team b |
| node05    | http://node05.company.com:4243 | team c |
| node06    | http://node06.company.com:4243 | team c |
+-----------+--------------------------------+--------+</code></pre>
<p>Based on this mapping, whenever a user of  <code>team a</code> runs a deployment of one of their applications, tsuru will create the container in <code>node01</code> or <code>node02</code>, never in any of the other nodes.</p>
<p>So, by using docker-cluster with a customized scheduler, tsuru is able to scale and segregate Docker containers, and handle Globo.com's production environment.</p>
