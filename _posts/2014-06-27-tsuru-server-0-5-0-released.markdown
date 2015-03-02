---
layout: post
status: publish
published: true
title: tsuru server 0.5.0 released!
author:
  display_name: andrews medina
  login: andrewsmedina
  email: andrewsmedina@gmail.com
  url: http://andrewsmedina.com
author_login: andrewsmedina
author_email: andrewsmedina@gmail.com
author_url: http://andrewsmedina.com
wordpress_id: 116
wordpress_url: http://blog.tsuru.io/?p=116
redirect_from:
  - /2014/06/27/tsuru-server-0-5-0-released/
date: '2014-06-27 18:13:11 -0300'
date_gmt: '2014-06-27 21:13:11 -0300'
categories:
- Release
tags:
- release
comments:
- id: 9
  author: tsuru server 0.5.1 is out! | tsuru blog
  author_email: ''
  author_url: http://blog.tsuru.io/2014/07/02/tsuru-server-0-5-1-is-out/
  date: '2014-07-02 16:32:03 -0300'
  date_gmt: '2014-07-02 19:32:03 -0300'
  content: "[&#8230;] release fixes a bug in the previous release: now applications
    are not locked on tsuru run. This is also the release that dropped collector and
    [&#8230;]"
- id: 10
  author: tsuru server 0.5.2 is out! | tsuru blog
  author_email: ''
  author_url: http://blog.tsuru.io/2014/07/08/tsuru-server-0-5-2-is-out/
  date: '2014-07-08 12:17:26 -0300'
  date_gmt: '2014-07-08 15:17:26 -0300'
  content: "[&#8230;] This release fixes some bugs introduced by the 0.5 release:
    [&#8230;]"
---
<p>We are pleased to announce tsr 0.5.0 and  the equivalent client version, tsuru cli 0.10.0 and tsuru-admin 0.4.0.</p>
<h2>What is tsuru?</h2>
<p>tsuru is an extensible and open source Platform as a Service software. And `tsr` is the binary of the tsuru server api.</p>
<h2>What’s new in tsr 0.5.0</h2>
<p>One of the main feature on this release is improve the stability and consitency of the tsuru API.</p>
<ul>
<li>prevent inconsitency caused by problems on deploy (<a href="https://github.com/tsuru/tsuru/issues/803">#803</a>) / (<a href="https://github.com/tsuru/tsuru/issues/804">#804</a>)</li>
<li>units information is not updated by collector (<a href="https://github.com/tsuru/tsuru/issues/806">#806</a>)</li>
<li>fixed log listener on multiple API hosts (<a href="https://github.com/tsuru/tsuru/issues/762">#762</a>)</li>
<li>prevent inconsitency caused by simultaneous operations in an application (<a href="https://github.com/tsuru/tsuru/issues/789">#789</a>)</li>
<li>prevent inconsitency cause by simultaneous <tt>env-set</tt> calls (<a href="https://github.com/tsuru/tsuru/issues/820">#820</a>)</li>
<li>store information about errors and identify flawed application deployments (<a href="https://github.com/tsuru/tsuru/issues/816">#816</a>)</li>
</ul>
<h3>Buildpack</h3>
<p>tsuru now supports deploying applications using <a href="https://devcenter.heroku.com/articles/buildpacks">Heroku Buildpacks</a>.</p>
<p>Buildpacks are useful if you’re interested in following Heroku’s best practices for building applications or if you are deploying an application that already runs on Heroku.</p>
<p>tsuru uses <a href="https://github.com/progrium/buildstep">Buildstep Docker</a> image to deploy applications using buildpacks. For more information, take a look at the buildpacks documentation page: <a href="http://docs.tsuru.io/en/stable/using/buildpacks.html">http://docs.tsuru.io/en/stable/using/buildpacks.html</a>.</p>
<h3><a href="https://github.com/tsuru/tsuru/blob/master/docs/releases/tsr/0.5.0.rst#other-features" name="user-content-other-features"></a>Other features</h3>
<ul>
<li>filter application logs by unit (<a href="https://github.com/tsuru/tsuru/issues/375">#375</a>)</li>
<li>support for deployments with archives, which enables the use of the <tt>pre-receive</tt> Git hook, and also deployments without Git (<a href="https://github.com/tsuru/tsuru/issues/458">#458</a>, <a href="https://github.com/tsuru/tsuru/issues/442">#442</a> and <a href="https://github.com/tsuru/tsuru/issues/701">#701</a>)</li>
<li>stop and start commands (<a href="https://github.com/tsuru/tsuru/issues/606">#606</a>)</li>
<li>oauth support (<a href="https://github.com/tsuru/tsuru/issues/752">#752</a>)</li>
<li>platform update command (<a href="https://github.com/tsuru/tsuru/issues/780">#780</a>)</li>
<li>support services with https endpoint (<a href="https://github.com/tsuru/tsuru/pull/812">#812</a>) / (<a href="https://github.com/tsuru/tsuru/pull/821">#821</a>)</li>
<li>grouping nodes by pool in segregate scheduler. For more information you can see the docs about the segregate scheduler: <a href="http://docs.tsuru.io/en/0.5.0/provisioners/docker/schedulers.html">segregate scheduler documentation</a>.</li>
</ul>
<h3><a href="https://github.com/tsuru/tsuru/blob/master/docs/releases/tsr/0.5.0.rst#platforms" name="user-content-platforms"></a>Platforms</h3>
<ul>
<li><a href="http://docs.tsuru.io/en/0.4.0//apps/deploy-hooks.html">deployment hooks</a> support for static and PHP applications (<a href="https://github.com/tsuru/tsuru/issues/607">#607</a>)</li>
<li>new platform: buildpack (used for buildpack support)</li>
</ul>
<h2><a href="https://github.com/tsuru/tsuru/blob/master/docs/releases/tsr/0.5.0.rst#backwards-incompatible-changes" name="user-content-backwards-incompatible-changes"></a>Backwards incompatible changes</h2>
<ul>
<li>Juju provisioner was removed. This provisioner was not being maintained. A possible idea is to use Juju in the future to provision the tsuru nodes instead of units</li>
<li>ELB router was removed. This router was used only by juju.</li>
<li><tt>tsr admin</tt> was removed.</li>
<li>The field <tt>units</tt> was removed from the collection <tt>apps</tt>. Information about units are now available in the provisioner. Now the unit state is controlled by provisioner. If you are upgrading tsuru from 0.4.0 or an older version you should run the MongoDB script bellow, where the docker collection name is the name configured by docker:collection in tsuru.conf:</li>
</ul>
<pre>var migration = function(doc) {
    doc.units.forEach(function(unit){
        db.docker.update({"id": unit.name}, {$set: {"status": unit.state}});
    });
};

db.apps.find().forEach(migration);</pre>
<ul>
<li>The scheduler collection has changed to group nodes by pool. If you are using this scheduler you shoul run the MongoDB script bellow:</li>
</ul>
<pre>function idGenerator(id) {
    return id.replace(/\d+/g, "")
}

var migration = function(doc) {
    var id = idGenerator(doc._id);
    db.temp_scheduler_collection.update(
        {teams: doc.teams},
        {$push: {nodes: doc.address},
         $set: {teams: doc.teams, _id: id}},
        {upsert: true});
}
db.docker_scheduler.find().forEach(migration);
db.temp_scheduler_collection.renameCollection("docker_scheduler", true);</pre>
<p>You can implement your own idGenerator to return the name for the new pools. In our case the idGenerator generates an id based on node name. It makes sense because we use the node name to identify a node group.</p>
<h2><a href="https://github.com/tsuru/tsuru/blob/master/docs/releases/tsr/0.5.0.rst#features-deprecated-in-050" name="user-content-features-deprecated-in-050"></a>Features deprecated in 0.5.0</h2>
<p>Beanstalkd queue backend will be removed in 0.6.0.</p>
<div id="docker">
<div id="backwards-incompatible-changes">
<h2> Installing and updating</h2>
<p>You can install tsr and tsuru client from our <a href="http://docs.tsuru.io/en/stable/install/client.html#using-the-ppa-ubuntu-only">ppa deb packages</a> or using <a href="http://docs.tsuru.io/en/stable/install/client.html#using-homebrew-mac-os-x-only">homebrew</a> (clients only).</p>
</div>
</div>
