---
layout: post
title: "How to update dependencies on OpenShift"
author: Alexander Todorov
date: 2012-02-18 01:00
comments: true
categories: ["Tips", "OpenShift"]
---

If you are already running some cool application on [OpenShift](http://openshift.redhat.com)
it could be the case that you have to update some of the packages installed as dependencies.
Here is an example for an application using the python-2.6 cartridge.


Pull latest upstream packages
-----------------------------

The most simple method is to update everything to the latest upstream versions. 

1. Backup! Backup! Backup!

        rhc-snapshot -a mycoolapp
        mv mycoolapp.tar.gz mycoolapp-backup-before-update.tar.gz

1. If you haven't specified any particular version in `setup.py` it will
look like this:

        ...
        install_requires=[
                        'monupco-openshift-express-python',
                        'MySQL-python',
                        'Markdown',
                       ],
        ...

1. To update simply push to OpenShift instructing it to rebuild your virtualenv:

        cd mycoolapp/
        touch .openshift/markers/force_clean_build
        git add .openshift/markers/force_clean_build
        git commit -m "update to latest upstream"
        git push

Voila! The environment hosting your application is rebuilt from scratch.

Keeping some packages unchanged
-------------------------------

Suppose that before the update you have `Markdown-2.0.1` and you want to keep it!
This is easily solved by adding versioned dependency to `setup.py`

        -       'Markdown',
        +       'Markdown==2.0.1',

If you do that OpenShift will install the same `Markdown` version when rebuilding your
application. Everything else will use the latest available versions.


**Note:** after the update it's recommended that you remove the 
`.openshift/markers/force_clean_build` file. This will speed up the push/build process
and will not surprise you with unwanted changes.


Update only selected packages
-------------------------

Unless your application is really simple or you have tested the updates, I suspect that
you want to update only selected packages. This can be done without rebuilding the whole
virtualenv. Use versioned dependencies in `setup.py` :

        -       'Markdown==2.0.1',
        -       'django-countries',
        +       'Markdown>=2.1',
        +       'django-countries>=1.1.2',

No need for `force_clean_build` this time. Just

        git commit && git push

At the time of writing my application was using `Markdown-2.0.1` and `django-countries-1.0.5`.
Then it updated to `Markdown-2.1.1` and `django-countires-1.1.2` which also happened to be
the latest versions.


**Note:** this will not work without `force_clean_build`

        -       'django-countries==1.0.5',
        +       'django-countries',


Warning
-------

OpenShift uses a local mirror of [Python Package Index](http://pypi.python.org).
It seems to be updated every 24 hours or so. Have this in mind if you want to update
to a package that was just released. It will not work!


---------------------------------------------------------------------------------

[*Alexander Todorov*](http://about.me/atodorov) is Monupco's founder and lead developer!

For an insight of available updates to you OpenShift applications give
Monupco a [try](https://monupco-otb.rhcloud.com/applications/mine/)!
It keeps generating new [advisories](http://monupco.com/advisories/) every day!

