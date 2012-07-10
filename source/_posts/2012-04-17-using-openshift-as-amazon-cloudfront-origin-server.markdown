---
layout: post
title: "Using OpenShift as Amazon CloudFront origin server"
date: 2012-04-17 17:30
comments: true
author: Alexander Todorov
categories: ['OpenShift', 'Amazon', 'CDN']
---

It's been several months after the start of [*Difio*](http://www.dif.io) and we started
migrating various parts of the platform to CDN. The first to go are static 01 like
CSS, JavaScript, images and such. In this article I will show you how to get started with 
*Amazon CloudFront* and *OpenShift*. It is very easy once you understand how it works.


Why CloudFront and OpenShift
----------------------------

*Amazon CloudFront* is cheap and easy to setup with virtually no maintenance.
The most important feature 04 that it can fetch content from any public website.
Integrating it together with *OpenShift* gives some nice benefits:

* All static assets are managed with Git and stored in the same place where the application
code and HTML is - easy to develop and deploy;
* No need for external service to host the static files;
* *CloudFront* will be serving the files so network load on *OpenShift* is minimal;
* Easy to manage versioned URLs because HTML and static assets are in the same repo - more on this later;



Object expiration
-----------------

*CloudFront* will cache your objects for a certain period and then expire them. Frequently
used objects are expired less often. Depending on the content you may want to update the cache
more or less frequently. In my case CSS and JavaScript files change rarely so I wanted to tell
CloudFront to not expire the files quickly. I did this by telling *Apache* to send a custom value for
the Expires header.


        $ curl http://d71ktrt2emu2j.cloudfront.net/static/v1/css/style.css -D headers.txt
        $ cat headers.txt 
        HTTP/1.0 200 OK
        Date: Mon, 16 Apr 2012 19:02:16 GMT
        Server: Apache/2.2.15 (Red Hat)
        Last-Modified: Mon, 16 Apr 2012 19:00:33 GMT
        ETag: "120577-1b2d-4bdd06fc6f640"
        Accept-Ranges: bytes
        Content-Length: 6957
        Cache-Control: max-age=31536000
        Expires: Tue, 16 Apr 2013 19:02:16 GMT
        Content-Type: text/css
        Strict-Transport-Security: max-age=15768000, includeSubDomains
        Age: 73090
        X-Cache: Hit from cloudfront
        X-Amz-Cf-Id: X558vcEOsQkVQn5V9fbrWNTdo543v8VStxdb7LXIcUWAIbLKuIvp-w==,e8Dipk5FSNej3e0Y7c5ro-9mmn7OK8kWfbaRGwi1ww8ihwVzSab24A==
        Via: 1.0 d6343f267c91f2f0e78ef0a7d0b7921d.cloudfront.net (CloudFront)
        Connection: close


All headers before Strict-Transport-Security come from the origin server.

Versioning
----------

Sometimes however you need to update the files and force *CloudFront* to update the content. 
The recommended way to do this is to use URL versioning and update the path to the files
which changed. This will force *CloudFront* to cache and serve the content under the new path
while keeping the old content available until it expires. This way your visitors will not be
viewing your site with the new CSS and old JavaScript. 

There are many ways to do this and there are some nice frameworks as well. For Python there is *webassets*.
I don't have many static files so I opted for no additional dependencies. Instead I will be updating the
versions by hand.

What comes to mind is using *mod_rewrite* to redirect the versioned URLs back to non versioned ones.
However there's a catch. If you do this *CloudFront* will cache the redirect itself, not the content.
The next time visitors hit *CloudFront* they will receive the cached redirect and follow it back to your
origin server, which is defeating the purpose of having CDN.

To do it properly you have to rewrite the URLs but still return a 200 response code and the
content which needs to be cached. This is done with *mod_proxy*: 

        RewriteEngine on
        RewriteRule ^VERSION-(\d+)/(.*)$ http://%{ENV:OPENSHIFT_INTERNAL_IP}:%{ENV:OPENSHIFT_INTERNAL_PORT}/static/$2 [P,L]


This .htaccess trick doesn't work on *OpenShift* though. *mod_proxy* is not enabled at the moment.
See [bug 812389](https://bugzilla.redhat.com/show_bug.cgi?id=812389) for more info.

Luckily I was able to use symlinks to point to the content. Here's how it looks:


        $ pwd
        /home/atodorov/difio/wsgi/static

        $ cat .htaccess
        ExpiresActive On
        ExpiresDefault "access plus 1 year"

        $ ls -l
        drwxrwxr-x. 6 atodorov atodorov 4096 16 Apr 21,31 o
        lrwxrwxrwx. 1 atodorov atodorov    1 16 Apr 21,47 v1 -> o

        settings.py:
        STATIC_URL = '//d71ktrt2emu2j.cloudfront.net/static/v1/'

        HTML template:
        {% raw %}<link type="text/css" rel="stylesheet" media="screen" href="{{ STATIC_URL }}css/style.css" />{% endraw %}


How to implement it
-------------------

First you need to split all CSS and JavaScript from your HTML if you haven't done so already. 

Then place everything under your git repo so that *OpenShift* will serve the files. For Python applications
place the files under wsgi/static/ directory in your git repo.


Point all of your HTML templates to the static location on *OpenShift* and test if everything works as expected. 
This is best done if you're using some sort of template language and store the location
in a single variable which you can change later.
*Difio* uses *Django* and the *STATIC_URL* variable of course.


Create your *CloudFront* distribution - don't use *Amazon S3*, instead configure a custom origin server. Write down
your *CloudFront* URL. It will be something like **1234xyz.cludfront.net**.

Every time a request hits *CloudFront* it will check if the object is present in the cache. If not present
*CloudFront* will fetch the object from the origin server and populate the cache. Then the object is sent
to the user.


Update your templates to point to the new cloudfront.net URL and redeploy your website!


---------------------------------------------------------------------------------

[*Alexander Todorov*](http://about.me/atodorov) is Difio's founder and lead developer!

For an insight of available updates to you OpenShift applications give
Difio a [try](https://difio-otb.rhcloud.com/applications/mine/)!
