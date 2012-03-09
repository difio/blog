---
layout: post
title: "How to get to the OpenShift shell"
date: 2012-03-09 21:43
comments: true
author: Alexander Todorov
categories: ["Tips", "OpenShift"]
---

I wanted to examine the Perl environment on OpenShift and got tired of making snapshots,
unzipping the archive and poking through the files. I wanted a shell. Here's how to get one.

1. Get the application info first

        $ rhc-domain-info 
        Password: 
        Application Info
        ================
        myapp
            Framework: perl-5.10
             Creation: 2012-03-08T13:34:46-04:00
                 UUID: 8946b976ad284cf5b2401caf736186bd
              Git URL: ssh://8946b976ad284cf5b2401caf736186bd@myapp-mydomain.rhcloud.com/~/git/myapp.git/
           Public URL: http://myapp-mydomain.rhcloud.com/
        
         Embedded: 
              None

1. The Git URL has your username and host

1. Now just ssh into the application

        $ ssh 8946b976ad284cf5b2401caf736186bd@myapp-mydomain.rhcloud.com
        
            Welcome to OpenShift shell
        
            This shell will assist you in managing OpenShift applications.
        
            !!! IMPORTANT !!! IMPORTANT !!! IMPORTANT !!!
            Shell access is quite powerful and it is possible for you to
            accidentally damage your application.  Proceed with care!
            If worse comes to worst, destroy your application with 'rhc app destroy'
            and recreate it
            !!! IMPORTANT !!! IMPORTANT !!! IMPORTANT !!!
        
            Type "help" for more info.
        
        [myapp-mydomain.rhcloud.com ~]\> 

**Voila!**

---------------------------------------------------------------------------------

[*Alexander Todorov*](http://about.me/atodorov) is Monupco's founder and lead developer!

For an insight of available updates to you OpenShift applications give
Monupco a [try](https://monupco-otb.rhcloud.com/applications/mine/)!
