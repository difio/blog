---
layout: post
title: "Difio is Open Source"
date: 2014-04-09 16:20
comments: true
categories: ['News']
---

[Difio](http://www.dif.io) is pleased to announce that we're now open source!
As [promised earlier](/2013/08/21/important-changes-to-difio-registration-subscriptions-open-source/)
the core service components and functionality have been made 
[available](https://github.com/difio/difio) under the
Apache Software License.

Difio is a Django based application which keeps track of packages and tells you
when they change. It provides multiple change analytics so you can make an informed
decision when or what to upgrade.

Difio is relatively large application which contains multiple components. Explanation
and example `settings.py` configuration has been provided in the
[README](https://github.com/difio/difio) file. The default settings are made to work
on a Linux/Unix system with minimum dependencies on external services. In a production
environment you will likely want to change these settings - for example file storage
server, messaging layer, email backend and caching layer to name a few.


The core difio/ application contains the logic for comparing package versions
and producing analytics between them as seen on [www.dif.io](http://www.dif.io). It is missing
the authentication backend(s) and user profile modules available in our SaaS
offering. You will have to plug your own code here.

We encourage developers to download and install Difio on their systems and
[report bugs and issues](https://github.com/difio/difio/issues/new) to us.
For development queries please use the
[difio-devel](https://groups.google.com/forum/#!forum/difio-devel) group.

