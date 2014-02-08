---
layout: post
title: "New Look and Feel for Application Info Pages"
date: 2013-02-21 00:42
comments: true
categories: ['News']
---

Today [Difio](http://www.dif.io) is pleased to announce new look and feel
for application info pages. Difio keeps track of application
dependencies and tells you when they change. We let you inspect the
changes and make informed decision when or what to upgrade.

![App Info Page](/images/new_app_info.png "App Info page")

Previously the application info page was showing only the latest available
updates. This made it hard for users to inspect older updates.
For example if you had Django-1.4.3 you would see the
latest Django-1.4.5 but not 1.4.4.


For packages which maintain several active branches it was not possible to
compare installed version against stable branch versions. It was always compared
to the latest from the master branch.
For example if you had ffi-1.3.0 you could not see ffi-1.3.1 but
would see ffi-1.4.0 instead.


Today's release fixes this by offering the user all available updates to
their packages. In addition change rate icons are replaced by color codes.
The version string is now shown as a button in one of the standard colors
green (low), orange (medium) or red (high). Improvement has been made to
the page load speed as well. It is now significantly faster.

Email notifications still display only the highest available version.
This will be changed soon to include intermediate versions.
At the moment information about intermediate versions is available only
via the web interface or [RSS](http://feeds.feedburner.com/difio/updates).

We encourage developers from all backgrounds and
languages to [register](http://www.dif.io/register/) their applications and
send us their feedback via [GitHub](https://github.com/difio/difio/issues/new)
or [Twitter](https://twitter.com/DifioNews).
