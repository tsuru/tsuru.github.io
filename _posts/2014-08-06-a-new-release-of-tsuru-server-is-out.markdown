---
layout: post
status: publish
published: true
title: A new release of tsuru server is out!
author:
  display_name: Francisco Souza
  login: francisco
  email: fss@corp.globo.com
  url: http://f.souza.cc
author_login: francisco
author_email: fss@corp.globo.com
author_url: http://f.souza.cc
excerpt: "tsuru server 0.6.0, along with <a href=\"http://docs.tsuru.io/en/latest/releases/tsuru/0.11.0.html\"
  title=\"tsuru 0.11.0\">tsuru client 0.11.0</a> and <a href=\"http://docs.tsuru.io/en/latest/releases/tsuru-admin/0.5.0.html\"
  title=\"tsuru-admin 0.5.0\">tsuru-admin 0.5.0</a>, is out today!\r\n\r\n<h2>What
  is tsuru?</h2>\r\ntsuru is an extensible and open source Platform as a Service software.
  <strong>tsr</strong> is the binary of the tsuru server api, while <strong>tsuru</strong>
  and <strong>tsuru-admin</strong> are clients of the server, used by application
  developers and cloud administrators, respectively.\r\n\r\n<h2>What’s new in tsr
  0.6.0</h2>\r\n\r\nThe main feature in this release is a better integration with
  infrastructure providers. tsuru is now able to provision Docker hosts on CloudStack
  and EC2, which mean that users can start a new cluster just by installing the server
  package and running some <code>tsuru-admin</code> commands to add new nodes to the
  cluster."
wordpress_id: 130
wordpress_url: http://blog.tsuru.io/?p=130
redirect_from:
  - /2014/08/06/a-new-release-of-tsuru-server-is-out/
date: '2014-08-06 17:06:37 -0300'
date_gmt: '2014-08-06 20:06:37 -0300'
categories:
- Release
tags:
- docker
- release
comments: []
---
<p>tsuru server 0.6.0, along with <a href="http://docs.tsuru.io/en/latest/releases/tsuru/0.11.0.html" title="tsuru 0.11.0">tsuru client 0.11.0</a> and <a href="http://docs.tsuru.io/en/latest/releases/tsuru-admin/0.5.0.html" title="tsuru-admin 0.5.0">tsuru-admin 0.5.0</a>, is out today!</p>
<h2>What is tsuru?</h2>
<p>tsuru is an extensible and open source Platform as a Service software. <strong>tsr</strong> is the binary of the tsuru server api, while <strong>tsuru</strong> and <strong>tsuru-admin</strong> are clients of the server, used by application developers and cloud administrators, respectively.</p>
<h2>What’s new in tsr 0.6.0</h2>
<p>The main feature in this release is a better integration with infrastructure providers. tsuru is now able to provision Docker hosts on CloudStack and EC2, which mean that users can start a new cluster just by installing the server package and running some <code>tsuru-admin</code> commands to add new nodes to the cluster.<a id="more"></a><a id="more-130"></a></p>
<p>Users upgrading their servers to tsr 0.6.0 should also update client versions of <b>tsuru-admin</b> and <b>tsuru</b> to 0.5.0 and 0.11.0, respectively.</p>
<h3>Relevant news</h3>
<ul>
<li>The ssh-agent is no more! Now tsuru generates an RSA key pair per container, and connects directly via SSH to the container using the generated private key</li>
<li>tsuru administrators are able to take advantage of this new SSH approach and connect directly via SSH to a specific container, by running the command <code>tsuru-admin ssh [container-id]</code></li>
<li>It's now possible to talk to IaaS providers and add new Docker nodes to tsuru from scratch. tsuru administrators can run commands like <code>tsuru-admin docker-node-add</code> and <code>tsuru-admin docker-node-remove</code> (please refer to the <a href="http://docs.tsuru.io/en/latest/reference/tsuru-admin.html" title="tsuru-admin usage guide">tsuru-admin usage guide</a> for more details).
<li>beanstalkd support has been removed, the API server will refuse to start if it's configured to use beanstalkd. Users should switch to Redis</li>
<li>Now service instances also have team owners. In order to get it working, users should run a <a href="https://gist.github.com/fsouza/5e65879c5547fe753f48">migration script</a> in the database</li>
</ul>
<p>For a full list of changes, check the <a href="http://docs.tsuru.io/en/latest/releases/tsr/0.6.0.html" title="tsuru server 0.6.0 release notes">release notes of tsuru server 0.6.0</a>.</p>
<h2>Contributors</h2>
<p>Besides the core team, this release was also powered by some contributors. And we want to thank them for helping getting tsuru server 0.6.0 out. Here is the list of contributors that helped in this version:</p>
<ul>
<li>Dan van Wijk</li>
<li>Pablo Aguiar</li>
</ul>
<h2>Grab it today!</h2>
<p>You can install or upgrade tsuru server <a href="http://docs.tsuru.io/en/latest/installing/api.html#adding-repositories">using our PPA</a> or building it from source. The clients are available both on Homebrew and in the PPA, for more details, check the <a href="http://docs.tsuru.io/en/latest/using/install-client.html" title="How to install tsuru clients">client installation docs</a>.</p>
