---
layout: post
status: publish
published: true
title: tsuru server 0.8.0 is out!
author:
  display_name: Francisco Souza
  login: francisco
  email: fss@corp.globo.com
  url: http://f.souza.cc
author_login: francisco
author_email: fss@corp.globo.com
author_url: http://f.souza.cc
wordpress_id: 181
wordpress_url: http://blog.tsuru.io/?p=181
date: '2014-10-21 15:10:09 -0200'
date_gmt: '2014-10-21 18:10:09 -0200'
categories:
- Release
tags:
- docker
- release
comments: []
---
<p>tsuru server 0.8.0, along with <a href="https://github.com/tsuru/tsuru-client/releases/tag/0.13.0" title="tsuru-client 0.13.0 release notes">tsuru client 0.13.0</a>, <a href="https://github.com/tsuru/tsuru-admin/releases/tag/0.7.0" title="tsuru-admin 0.7.0 release notes">tsuru-admin 0.7.0</a> and <a href="https://github.com/tsuru/crane/releases/tag/0.6.0" title="crane 0.6.0 release notes">crane 0.6.0</a>, is out today!</p>
<p>The main feature of this release is the new application plan support: now apps can be associated to plans, that define the amount of memory and CPU shares that units of the application will have. The container scheduler has been adjusted to respect these limits when scheduling new containers, so containers will born in hosts with the largest amount of available resources.</p>
<p>Other features worth highlighting:</p>
<ul>
<li>support for multiple CloudStack and Amazon EC2 regions, via <a href="http://docs.tsuru.io/en/0.8.0/reference/config.html#custom-iaas">custom IaaS configuration</a></li>
<li>actual support for removing platforms from tsuru, there was a bug in previous version that prevented the platform from being removed from the database</li>
<li>changes in the behavior of "app-restart", "env-set" and "env-get". Now these commands log their progress, as they go through some steps, like adding new units, waiting for them to become responsive and removing the old ones</li>
<li>major rename of commands in the tsuru client. We've standardized the commands in the pattern &lt;subject&gt;-&lt;action&gt;, so "restart" became "app-restart", "log" became "app-log", "add-cname" became "cname-add", and so on. Check <a href="https://github.com/tsuru/tsuru-client/releases/tag/0.13.0" title="tsuru-client 0.13.0 release notes">tsuru 0.13.0 release notes</a> for more details</li>
</ul>
<p>You can see the complete list of features in the <a href="http://docs.tsuru.io/en/0.8.0/releases/tsr/0.8.0.html" title="tsr 0.8.0 release notes">release notes of tsuru server 0.8.0</a>.</p>
<h2>Contributors</h2>
<p>Besides the core team, this release was also powered by some contributors. And we want to thank them for helping getting tsuru server 0.8.0 out. Here is the list of contributors that helped in this version:</p>
<ul>
<li>Flavia Missi</li>
<li>Josh Blancett</li>
</ul>
<h2>Grab it today!</h2>
<p>You can install or upgrade tsuru server <a href="http://docs.tsuru.io/en/0.8.0/installing/api.html#adding-repositories">using our PPA</a> or building it from source. The clients are available on Homebrew, GitHub and in the PPA, for more details, check the <a href="http://docs.tsuru.io/en/0.8.0/using/install-client.html">client installation docs</a>.</p>
