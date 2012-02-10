---
layout: post
title: "Spinning-up a development instance on OpenShift Express"
date: 2012-02-10 21:19
comments: true
categories: ["Tips", "OpenShift"]
---

[Monupco](http://monupco.com) is hosted on [OpenShift](http://openshift.redhat.com) Express.
During development we often need to spin-up another copy of Monupco to use for testing and development.
With OpenShift this is easy and fast. Here's how:

1. Create another application on OpenShift. This will be your development instance.

        rhc-create-app -a myappdevel -t python-2.6

1. Find out the git url for the production application:

        $ rhc-user-info
        Application Info
        ================
        myapp
            Framework: python-2.6
             Creation: 2012-02-10T12:39:53-05:00
                 UUID: 723f0331e17041e8b34228f87a6cf1f5
              Git URL: ssh://723f0331e17041e8b34228f87a6cf1f5@myapp-mydomain.rhcloud.com/~/git/myapp.git/
           Public URL: http://myapp-mydomain.rhcloud.com/

1. Push the current code base from the production instance to devel instance:

        cd myappdevel
        git remote add production -m master ssh://723f0331e17041e8b34228f87a6cf1f5@myapp-mydomain.rhcloud.com/~/git/myapp.git/
        git pull -s recursive -X theirs production master
        git push

1. Now your `myappdevel` is the same as your production instance. You will probably want to
modify your database connection settings at this point and start adding new features.
