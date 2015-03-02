---
layout: post
status: publish
published: true
title: Tsuru server 0.7.0 is out!!
author:
  display_name: Tarsis Azevedo
  login: tarsis
  email: tarsis@corp.globo.com
  url: http://tarsisazevedo.com
author_login: tarsis
author_email: tarsis@corp.globo.com
author_url: http://tarsisazevedo.com
wordpress_id: 153
wordpress_url: http://blog.tsuru.io/?p=153
redirect_from:
  - /2014/09/23/tsuru-server-0-7-0-is-out/
date: '2014-09-23 11:04:32 -0300'
date_gmt: '2014-09-23 14:04:32 -0300'
categories:
- Release
tags: []
comments:
- id: 12
  author: Magno Alexandre Torres
  author_email: magnotorres@gmail.com
  author_url: http://www.magnotorres.com.br
  date: '2014-09-23 19:18:00 -0300'
  date_gmt: '2014-09-23 22:18:00 -0300'
  content: Great Bonus Feature!  o/
- id: 13
  author: rualatngua
  author_email: donga.spirit@gmail.com
  author_url: ''
  date: '2014-09-24 01:15:00 -0300'
  date_gmt: '2014-09-24 04:15:00 -0300'
  content: Great release.
- id: 14
  author: Danilo Bardusco
  author_email: bardusco@gmail.com
  author_url: ''
  date: '2014-09-24 23:50:00 -0300'
  date_gmt: '2014-09-25 02:50:00 -0300'
  content: Congrats team!
---
<p>tsuru server 0.7.0, along with tsuru client 0.12.0 and tsuru-admin 0.6.0, is out today!</p>
<p>The main feature in this release is the new command <strong>tsuru deploy</strong> which allows you to deploy a set of files and/or a directory and/or a binary file to tsuru directly without using git.</p>
<p>It's useful when you need to build a lot of things, so you can build it locally and deploy to tsuru directly, making your <strong>deploy faster and easier</strong>. For instance, you can build a java project and just deploy your .WAR file (<strong>tsuru deploy yourproject.war</strong>) or deploy an entire directory without git (<strong>tsuru deploy .</strong>).</p>
<p>Other new features worth highlighting are:</p>
<ul>
<li>
        It’s now possible for an app to have multiple cnames. The <strong>tsuru set-cname</strong> and <strong>tsuru unset-cname</strong> have been removed and <strong>tsuru add-cname</strong> and <strong>tsuru remove-cname</strong> were added.
    </li>
<li>
        tsuru is now able to heal failing nodes and containers automatically, this is disabled by default. Instructions can be found in the <a href="http://docs.tsuru.io/en/stable/reference/config.html#config-healing">config reference</a>.
    </li>
<li>
        It’s possible to configure a health check request path to be called during the deployment process of an application. See <a href="http://docs.tsuru.io/en/stable/using/tsuru.yaml.html#yaml-healthcheck">health check docs</a> for more details.
    </li>
</ul>
<p>You can <strong>see other cool features</strong> in <a href="http://docs.tsuru.io/en/stable/releases/tsr/0.7.0.html">this release here</a>.</p>
<h2>Bonus Feature</h2>
<p>Now, tsuru has responsive tables!!! \o/</p>
<p><img src="http://i.imgur.com/dtS3TBA.gif" /></p>
<p><img src="https://camo.githubusercontent.com/92a0e6c8cfa3aae0e70f442fc915263ee59bf5bf/687474703a2f2f6d656469612e74756d626c722e636f6d2f74756d626c725f6c74757a6a766251364c31717a677078392e676966" /></p>
<h2>Contributors</h2>
<p>Besides the core team, this release was also powered by some contributors. And we want to thank them for helping getting tsuru server 0.7.0 out. Here is the list of contributors that helped in this version:</p>
<ul>
<li>Diego Toral</li>
<li>Marc Abramowitz</li>
<li>Thinh Nguyen</li>
</ul>
<h2>Grab it today!</h2>
<p>You can install or upgrade tsuru server <a href="http://docs.tsuru.io/en/stable/installing/api.html#adding-repositories">using our PPA</a> or building it from source. The clients are available both on Homebrew and in the PPA, for more details, check the <a href="http://docs.tsuru.io/en/stable/using/install-client.html">client installation docs</a>.</p>
