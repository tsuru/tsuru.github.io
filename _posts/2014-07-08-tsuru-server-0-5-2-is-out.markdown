---
layout: post
status: publish
published: true
title: tsuru server 0.5.2 is out!
author:
  display_name: Francisco Souza
  login: francisco
  email: fss@corp.globo.com
  url: http://f.souza.cc
author_login: francisco
author_email: fss@corp.globo.com
author_url: http://f.souza.cc
wordpress_id: 125
wordpress_url: http://blog.tsuru.io/?p=125
redirect_from:
  - /2014/07/08/tsuru-server-0-5-2-is-out/
date: '2014-07-08 12:17:23 -0300'
date_gmt: '2014-07-08 15:17:23 -0300'
categories:
- Release
tags: []
comments: []
---
<p>We've just released tsuru server 0.5.2.</p>
<p>This release fixes some bugs introduced by the <a href="http://blog.tsuru.io/2014/06/27/tsuru-server-0-5-0-released/" title="tsuru 0.5.0 released">0.5 release</a>:</p>
<ul>
<li>applications are now properly locked on <code>unit-remove</code>.</li>
<li>fix race condition on <code>unit-remove</code> that prevented it from removing more than one unit at once</li>
<li>properly report errors when removing a Docker node that does not exist in the cluster</li>
</ul>
<p>It also includes some minor improvements, for more details, take a look at the <a href="http://docs.tsuru.io/en/stable/releases/tsr/0.5.2.html" title="tsuru server 0.5.2 release notes">release notes for tsuru 0.5.2</a>.</p>
