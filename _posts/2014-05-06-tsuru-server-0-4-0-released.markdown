---
layout: post
status: publish
published: true
title: tsuru server 0.4.0 released!
author:
  display_name: andrews medina
  login: andrewsmedina
  email: andrewsmedina@gmail.com
  url: http://andrewsmedina.com
author_login: andrewsmedina
author_email: andrewsmedina@gmail.com
author_url: http://andrewsmedina.com
wordpress_id: 91
wordpress_url: http://blog.tsuru.io/?p=91
redirect_from:
  - /2014/05/06/suru-server-0-4-0-released/
date: '2014-05-06 11:15:57 -0300'
date_gmt: '2014-05-06 14:15:57 -0300'
categories:
- Release
tags:
- docker
- release
comments:
- id: 6
  author: tsuru server 0.4.0 released! | tsuru blog | Doc...
  author_email: ''
  author_url: http://www.scoop.it/t/docker-by-docker/p/4020851564/2014/05/06/tsuru-server-0-4-0-released-tsuru-blog
  date: '2014-05-06 12:22:46 -0300'
  date_gmt: '2014-05-06 15:22:46 -0300'
  content: "[&#8230;] We are pleased to announce tsr 0.4.0 and the equivalent client
    version, tsuru cli 0.9.0 and tsuru-admin 0.3.0.&nbsp; [&#8230;]"
---
<p>We are pleased to announce tsr 0.4.0 and  the equivalent client version, tsuru cli 0.9.0 and tsuru-admin 0.3.0.</p>
<h2>What is tsuru?</h2>
<p>tsuru is an extensible and open source Platform as a Service software. And `tsr` is the binary of the tsuru server api.</p>
<h2>What’s new in tsr 0.4.0</h2>
<p>There are a lot of changes since the 0.3.0 version:</p>
<h4>New Redis queue backend.</h4>
<p>Now you can use Redis instead of beanstalk for work queue. In order to use Redis, you need to change the configuration file:</p>
<div>
<div>
<pre>queue: redis
redis-queue:
  host: "localhost"
  port: 6379
  db: 4
  password: "your-password"</pre>
</div>
</div>
<p>All settings are optional (<tt>queue</tt> will still be default to “beanstalkd”), refer to <a href="http://docs.tsuru.io/en/stable/config.html">configuration docs</a> for more details.</p>
<div id="docker">
<h4>Docker</h4>
<ul>
<li>Refactored unit creation to be more atomic</li>
<li>Support for unit-agent (<a href="https://github.com/tsuru/tsuru/issues/633">#633</a>) - tsuru unit agent repository: <a href="https://github.com/tsuru/tsuru-unit-agent">https://github.com/tsuru/tsuru-unit-agent</a></li>
<li>Added an administrative command to move and rebalance containers between nodes (<a href="https://github.com/tsuru/tsuru/issues/646">#646</a>) - docs about rebalance: <a href="http://docs.tsuru.io/en/stable/apps/tsuru-admin/usage.html#containers-rebalance">http://docs.tsuru.io/en/stable/apps/tsuru-admin/usage.html#containers-rebalance</a></li>
<li>ram  and swap memory limit is configurable (<a href="https://github.com/tsuru/tsuru/issues/764">#764</a> and <a href="https://github.com/tsuru/tsuru/issues/434">#434</a>)</li>
<li>Added a command to add a new platform (<a href="https://github.com/tsuru/tsuru/issues/780">#780</a>) - docs about <cite>platform-add</cite> command: <a href="http://docs.tsuru.io/en/stable/apps/tsuru-admin/usage.html#platform-add">http://docs.tsuru.io/en/stable/apps/tsuru-admin/usage.html#platform-add</a></li>
<li>Do not restart on unit-add (nor unit-remove)</li>
<li>Improved debug logs for SSH - <a href="https://github.com/tsuru/tsuru/issues/665">#665</a></li>
<li>Fixed URL for listing containers by app</li>
<li>Deploy hook support enviroment variables with space</li>
<li>Always pull the image before creating the container</li>
</ul>
<div id="api">
<h4>API</h4>
<ul>
<li>Added app team owner - <a href="https://github.com/tsuru/tsuru/issues/619">#619</a></li>
<li>Exposed public url in <cite>create-app</cite> - <a href="https://github.com/tsuru/tsuru/issues/724">#724</a></li>
<li>Improved feedback for duplicated users - <a href="https://github.com/tsuru/tsuru/issues/693">#693</a></li>
<li>Login expose <cite>is_admin</cite> info</li>
<li>Improve output of the get environment variables endpoint</li>
<li>Exposed deploys of the app in the app-info API</li>
<li>Improved administrative API for the Docker provisioner</li>
<li>Stored deploy metadata</li>
<li>Improved healthcheck (ping MongoDB before marking the API is ok)</li>
<li>Exposed owner of the app in the app-info API</li>
</ul>
<h4>Services</h4>
<ul>
<li>Added support for plans</li>
<li>New experimental varnish service - <a href="https://github.com/tsuru/varnishapi">https://github.com/tsuru/varnishapi</a></li>
<li>New experimental health check service, with the zabbix support - <a href="https://github.com/tsuru/healthcheck-as-a-service">https://github.com/tsuru/healthcheck-as-a-service</a></li>
<li>Several improvements on redis service, with support to an isolated and high available redis service, using docker and sentinel: <a href="https://github.com/tsuru/redisapi">https://github.com/tsuru/redisapi</a></li>
</ul>
<h4>Platforms</h4>
<ul>
<li>New Python 3 platform</li>
<li>New Go platform</li>
<li>Support to syslog</li>
<li>When a process restarts too often, we say that it is <em>flapping</em>. Now we keep track of worker restarts and stops the corresponding process in case it is flapping</li>
</ul>
</div>
<h4>tsuru client changes</h4>
<ul>
<li>Fixed output when service doesn’t export environment variables (<a href="https://github.com/tsuru/tsuru/issues/772">#772</a>)</li>
<li>Swap address and cname on apps when running swap</li>
<li>App owner team is configurable - <a href="https://github.com/tsuru/tsuru/issues/620">#620</a></li>
<li>New plugin system - <a href="https://github.com/tsuru/tsuru/issues/620">#737</a> - Now it is possible customize tsuru client, installing and creating plugins. <a href="http://docs.tsuru.io/en/stable/using/cli/plugins.html">See the docs for more info</a></li>
</ul>
<div id="backwards-incompatible-changes">
<h2>Backwards incompatible changes</h2>
<p>The S3 integration on app creation was removed. The config properties <cite>bucket-support</cite>, <cite>aws:iam</cite> <cite>aws:s3</cite> were removed too.</p>
<p>All existing apps have no team owner. You can run the MongoDB script below to automatically set the first existing team in the app as team owner.</p>
<div>
<div>
<pre>db.apps.find({ teamowner: { $exists: false }}).forEach(
    function(app) {
        app.teamowner = app.teams[0];
        db.apps.save(app);
    }
);</pre>
</div>
</div>
<h2> Installing and updating</h2>
<p>You can install tsr and tsuru client from our <a href="http://docs.tsuru.io/en/stable/install/client.html#using-the-ppa-ubuntu-only">ppa deb packages</a> or using <a href="http://docs.tsuru.io/en/stable/install/client.html#using-homebrew-mac-os-x-only">homebrew</a> (clients only).</p>
</div>
</div>
