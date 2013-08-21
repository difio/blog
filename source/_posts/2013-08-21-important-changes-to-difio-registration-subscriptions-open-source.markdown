---
layout: post
title: "Important Changes To Difio - Registration, Subscriptions and Open Source"
date: 2013-08-21 15:47
comments: true
author: Alexander Todorov, Lead Developer
categories: ['News']
---


As [Difio](http://www.dif.io)'s Lead Developer and on behalf of the Difio team,
it is my pleasure to announce today our future plans for Difio. This is a high
level outline of pending changes which will be implemented in the upcoming
weeks. Each of them will be announced in more details later.

Easier App Registration
------------------------

Currently there are several ways to register applications into Difio, both
manual and automated and several popular PaaS providers are supported.
Automated registration is done via script, which needs to be installed and
configured into your environment. This proved to be confusing and hard to use.

We're changing the registration model to read your app dependencies from
a publicly accessible URL containing your requirements.txt, Gemfile, etc.
You will have the flexibility to create your own script to refresh this file
contents, no more installing extra packages from us.

Cloud related registration methods will be updated as well and refactored
as plugins modeled after the cloud vendor's specifications.

Existing app registrations will be migrated to work appropriately.

Together with this feature Difio will introduce much wanted from everyone
integration with GitHub and BitBucket.

Changes To Subscription Model
------------------------------

The present subscription model requires payment if you'd like to access
[additional upgrade analytics](http://www.dif.io/add-on/). This will change.
Add-ons will be accessible free of charge! 

The paid subscription will cover
access to analytics for older packages. 
After all Difio is here to help your apps stay up-to-date. 
We're currently thinking about a
one year cut-off based on the package release date.


Open Source Here We Come
------------------------

Everyone involved with Difio (both users and developers) has their roots in
the open source movement, myself included. We're going to open source as much as
possible of our platform!

At first all [add-on tests](http://www.dif.io/add-on/) will be refactored and
made open. Our goal is this to coincide or closely follow the changes of the
subscription model and have both open source and free of charge analytics.

Following this event other parts of the platform will be open sourced gradually
where appropriate.


Other Minor Changes
-------------------

Since the announced changes will touch base with lots of Difio's internal
components we will use the opportunity to refresh some extra code as well
like the user interface and the email notification sub-system. All changes
will be announced in our newsletter.


I can't wait to start writing code and transforming the platform in response to
your great feedback. In the mean time enjoy [Difio](http://www.dif.io) and
keep your apps up-to-date!

---
Alexander Todorov, Lead Developer<br/>
[@atodorov_](http://twitter.com/atodorov_)
