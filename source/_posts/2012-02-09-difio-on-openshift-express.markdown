---
layout: post
title: "Monupco on OpenShift Express"
date: 2012-02-09 18:48
author: Alexander Todorov
comments: true
categories: OpenShift
---

[Monupco](http://www.monupco.com) stands for Monitor Updates In The Cloud.
As the name suggests this is a service which provides updates information
for applications hosted in a PaaS environment. If you are a developer or
a sysadmin knowing when and what to upgrade will make your life easier.

Monupco will generate a human friendly description of changes between the
installed package version and the latest one. Currently a [client
side tool](https://github.com/monupco/monupco-openshift-express-python) for
Python applications on OpenShift Express is available and
others will follow soon.


Monupco started with a local SQLite database which was the fastest way to get up
and running. At present the database layer is powered by MySQL and the intention
is to switch to NoSQL at some point. It is written in Python.

Monupco is split into several parts:

* Management console - the interface with which users interact.
It is hosted on [OpenShift](http://openshift.redhat.com/) Express.
* Website - static HTML website which is periodically updated by a
[Celery](http://celeryproject.org/) task.
* Blog - powered by [Octopress](http://octopress.org). Together with
the website this is hosted on GitHub.


All source code of Monupco is managed with git and 'git push' is simply a
rock star. Combining git + ssh keys made it possible to programatically commit
and push when necessary.

The application uses Markdown extensively. All blog and website pages
and multi-line text entries into the database are rendered as Markdown.
This makes entering and editing text very easy.


While developing Monupco I didn't want to force users to remember yet another
username and password nor store them into the database. The solution is no passwords required!
Instead Monupco uses popular social networks credentials and limits the information
stored in database to the bare minimum.



Monupco has recently [announced](http://monupco.com/blog/2012/02/06/monupco-1.1-release-announcement/)
its first Alpha release. The following weeks will see development for Ruby, PHP and Perl packages
and the corresponding client side tools for these catridges on OpenShift. 
Java and Node.js are also under investigation.

Once these popular languages and package types are supported, client side tools
for other PaaS vendors will follow. On the radar are requests for:

* Heroku
* Engine Yard
* AppFog
* Google Apps Engine
* SalesForce
* DotCloud


If you're already excited please follow @monupco on [Twitter](https://twitter.com/monupco) and
[GitHub](https://github.com/monupco) or [get started](https://monupco-otb.rhcloud.com/applications/mine/) today!
