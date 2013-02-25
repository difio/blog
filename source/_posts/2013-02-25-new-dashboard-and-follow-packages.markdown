---
layout: post
title: "New Dashboard and Follow Packages Functionality"
date: 2013-02-25 11:55
comments: true
categories: ['News']
---

Today [Difio](http://www.dif.io) is pleased to announce our new dashboard
and the ability to follow packages without registering applications. Read
below for more information.

**Latest Releases**

![Latest Releases](/images/new_dashboard/releases.png "Latest Releases")

The default dashboard page is showing a news stream of all latest releases
for packages the user is following or using inside applications.


**Change History**

![Change History](/images/new_dashboard/change_history.png "Change History")

This page is showing a news stream of change analysis between multiple package
versions that the user is following or using inside applications. As shown in this
example the user is following `bundler-1.2.1` and `bundler-1.2.3` while the latest
available is `bundler-1.3.0` and `bundler-1.2.5`.


**Follow Packages**

![Follow Packages](/images/new_dashboard/follow.png "Follow Packages")

A new page to view and search packages is now available. Users can follow or unfollow
any packages and versions they want through the buttons. Simple color codes
distinguish between different states: green - user is following version;
gray - version is used inside registered application; transparent - not following version.
Versions which are used inside applications can only be removed/unfollowed by deleting
the entire application, or deleting the package from the application.
For example `Pygments-1.5` is been used in an application, but `Pygments-1.6` is been
followed manually.

It is highly recommended to follow a particular version, not only the package name.
If a user decides to follow only package name, but not versions, Difio will not be
able to generate change analysis reports because there's no
basis to compare to. In this case the user will be able to see only the latest
releases news stream.


**Applications**

This page is showing all registered applications for which Difio is monitoring dependencies.
This page has been available previously and also includes the improvements
[announced last week](/blog/2013/02/21/new-look-feel-application-info-pages/).
Small speed improvements have been made to this page as well.



**Invite Friends**

This is an interactive dialog which allows you to invite your fellows to try Difio.
It only asks for the email addresses of your friends and sends them an invitation.
We do not keep track of these addresses nor send any spam to them.

---

We encourage developers from all supported backgrounds and
languages to [start following packages](https://difio-otb.rhcloud.com/dashboard/follow/)
and send us their feedback via [GitHub](https://github.com/difio/bugs/issues/new)
or [Twitter](https://twitter.com/DifioNews).
