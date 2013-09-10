---
layout: post
title: "Latest Changes and Deprecated Functionality"
date: 2013-09-10 23:12
comments: true
categories: ['News']
---

Hey everyone,
[Difio](http://www.dif.io) is always hard at work to improve our package
tracking and updates analytics service. This is what we have been working on
lately:

Redesigned Application Dashboard
--------------------------------

We have redesigned the application dashboard which now shows
icons based on your programming language and a text status for each app,
telling you how many packages are outdated and how many are older than one year.
Check the picture below or 
[login to see yours](https://difio-otb.rhcloud.com/dashboard/).

!["New Apps Dashboard"](/images/new_app_dashboard.png "New Apps Dashboard")


Refreshed App Details View
--------------------------

The application details view has also been refreshed a bit! Non-essential fields
were removed for less clutter and new color code has been activated.
Installed packages are now colored in orange or red if they are older than six
months or one year respectively. This is an indication that dependencies may
be becoming stale and you have to plan your upgrade path soon. 

!["New App Details View"](/images/new_app_details.png "New App Details View")

Notification Email Changes
---------------------------

The daily and weekly notification digest emails were updated to specify applications
affected by each particular update. This feature has been requested by our community
of users and we were very happy to finally implement it!

To view your updates analytics you will have to 
[login into your dashboard](https://difio-otb.rhcloud.com/dashboard/). Links to
individual update analytics are no longer sent via email.


Follow Packages is Deprecated
------------------------------

Unfortunately the Follow Packages functionality had to go!
A very few people were using it
and where possible we have converted their records to individual applications.

Previously it was possible to follow a package without specifying any particular
version of it. There were only 56 such objects in our database which were not converted.



What's Next
------------

Last month Difio
[has announced](/blog/2013/08/21/important-changes-to-difio-registration-subscriptions-open-source/)
a road-map for the future. We're going to continue working on this and bring you
an easier and smoother application import next time.

In the mean time, don't forget to check your updates and upgrade your apps!




