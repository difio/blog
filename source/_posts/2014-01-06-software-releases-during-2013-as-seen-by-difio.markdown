---
layout: post
title: "Software Releases During 2013 as Seen by Difio"
date: 2014-01-06 10:05
comments: true
categories: ['news']
---

Happy New Year everyone! [Difio](http://www.dif.io) wishes you more bug-free
upgrades and more frequent deployments during 2014. In this blog post we're going
to summarize the previous year as seen by our updates analytics service.


23% Newly Released Packages
---------------------------

Difio continuously monitors upstream package release feeds and notification hooks
across six different programming languages. In 2013 there were **346914**
new package versions of which **80135** are newly created packages, which
didn't exist before. The rest are new version releases to already existing
software.

A fraction of these have been deployed by users of Difio which lead to a total
of **13077** analytics processed by our service.



Release Activity
----------------

In 2013 three languages stand out as being most actively used to develop new
software or improving existing packages:

* Node.js -  **143 thousand** package versions;
* Ruby - **102 thousand** package versions;
* Python - **61 thousand** package versions.

The top 5 packages which produced the highest number of new versions during 2013 are

* [tendenci](https://pypi.python.org/pypi/tendenci) - 238 versions
* [confine-controller](https://pypi.python.org/pypi/confine-controller) - 224 versions
* [fis](https://npmjs.org/package/fis) - 218 versions
* [riemann-babbler](https://rubygems.org/gems/riemann-babbler) - 214 versions
* [abaaso](https://npmjs.org/package/abaaso) - 204 versions


The most prolific months for developers turned out to be **April**, **March** and **December**,
producing over **34 thousand releases** each month. Some **6000** package versions were released
between Christmas and New Year's Eve alone!


Language Popularity
-------------------

Developers tracking their applications at Difio prefer Ruby and Python,
while Node.js comes third. The most frequently analyzed packages in each
language are

* Ruby - guard(155), newrelic_rpm(154), excon(151), sass(132), guard-rspec(127);
* Python - raven(259), boto(190), celery(185), billiard(181), kombu(177). The famous
Django framework comes sixth with 162 analytics processed by Difio;
* Node.js - browserify(214), connect(132), uglify-js(125), request(99), express(80).


From all we can tell important packages like web frameworks are kept more consistent
with respect to version usage while auxiliary packages and dependencies vary greatly
across deployed versions.


Are we missing something? Let us know and we will do some coding magic to extract
the information from our database. Happy New Year!
