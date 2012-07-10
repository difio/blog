---
layout: post
title: "OpenShift Cron Takes Over Celerybeat"
date: 2012-03-14 20:48
comments: true
author: Alexander Todorov
categories: ["Tips", "OpenShift", "Celery"]
---

[*Celery*](http://celeryproject.org/) is an asynchronous task queue/job queue
based on distributed message passing. You can define tasks as Python functions,
execute them in the background and in a periodic fashion.
[*Difio*](http://www.dif.io) uses *Celery* for virtually everything.
Some of the tasks are scheduled after some event takes place (like user pressed a button)
or scheduled periodically.


*Celery* provides several components of which *celerybeat* is the periodic task scheduler.
When combined with [*Django*](http://djangoproject.com) it gives you a very nice admin interface
which allows periodic tasks to be added to the scheduler.

Why change
----------

*Difio* has relied on *celerybeat* for a couple of months. Back then, when *Difio* launched,
there was no cron support for OpenShift so running *celerybeat* sounded reasonable.
It used to run on a dedicated virtual server and for most of the time that was fine. 

There were a number of issues which *Difio* faced during its first months:

* *celerybeat* would sometime die due to no free memory on the virtual instance.
When that happened no new tasks were scheduled and data was left unprocessed.
Let alone that higher memory instance and the processing power which comes with it
cost extra money.

* *Difio* is split into several components which need to have the same code base
locally - the most important are database settings and the periodic tasks
code. At least in one occasion *celerybeat* failed to start because of a buggy 
task code. The offending code was fixed in the application server on OpenShift but
not properly synced to the *celerybeat* instance. Keeping code in sync is a priority
for distributed projects which rely on *Celery*.

* *Celery* and *django-celery* seem to be updated quite often. This poses a significant risk
of ending up with different versions on the scheduler, worker nodes and the app server. This will
bring the whole application to a halt if at some point a backward incompatible change is introduced
and not properly tested and updated. Keeping infrastructure components in sync can be a big challenge
and I try to minimize this effort as much as possible.

* Having to navigate to the admin pages every time I add a new task or want to change the execution
frequency doesn't feel very natural for a console user like myself and IMHO is less productive.
For the record I primarily use *mcedit*. I wanted to have something more close to the
write, commit and push work-flow.


The take over
-------------

It's been some time since OpenShift
[introduced](https://www.redhat.com/openshift/community/blogs/getting-started-with-cron-jobs-on-openshift)
the cron cartridge and I decided to give it a try.

The first thing I did is to write a simple script which can execute any task from the difio.tasks module
by piping it to the Django shell (a Python shell actually).

    $ cat run_celery_task 
    
    #!/bin/bash
    #
    # Copyright (c) 2012, Alexander Todorov <atodorov@nospam.otb.bg>
    #
    # This script is symlinked to from the hourly/minutely, etc. directories
    #
    # SYNOPSIS
    #
    # ./run_celery_task cron_search_dates
    #
    # OR
    #
    # ln -s run_celery_task cron_search_dates
    # ./cron_search_dates
    #
    
    TASK_NAME=$1
    [ -z "$TASK_NAME" ] && TASK_NAME=$(basename $0)
    
    if [ -n "$OPENSHIFT_APP_DIR" ]; then
        source $OPENSHIFT_APP_DIR/virtenv/bin/activate
        export PYTHON_EGG_CACHE=$OPENSHIFT_DATA_DIR/.python-eggs
        REPO_DIR=$OPENSHIFT_REPO_DIR
    else
        REPO_DIR=$(dirname $0)"/../../.."
    fi
    
    echo "import difio.tasks; difio.tasks.$TASK_NAME.delay()" | $REPO_DIR/wsgi/difio/manage.py shell



This is a multicall script which allows symlinks with different names to point to it. 
Thus to add a new task to cron I just need to make a symlink to the script from one of the
hourly, minutely, daily, etc. directories under cron/

The script accepts a parameter as well which allows me to execute it locally for debugging purposes
or to schedule some tasks out of band.

This is how it looks like on the file system:

    $ ls -l .openshift/cron/hourly/
    some_task_name -> ../tasks/run_celery_task
    another_task -> ../tasks/run_celery_task


After having done these preparations I only had to embed the cron cartridge and git push to OpenShift:

    rhc-ctl-app -a difio -e add-cron-1.4 && git push


What's next
---------

At present OpenShift can schedule your jobs every minute, hour, day, week or month and does so using the
*run-parts* script. You can't schedule a script to execute at 4:30 every Monday or every 45 minutes for example.
See [rhbz #803485](https://bugzilla.redhat.com/show_bug.cgi?id=803485) if you want to follow the
progress. Luckily *Difio* doesn't use this sort of job scheduling for the moment.


*Difio* is scheduling periodic tasks from OpenShift cron for a few days already. 
It seems to work reliably and with no issues. One less component to maintain and worry about.
More time to write code.


---------------------------------------------------------------------------------

[*Alexander Todorov*](http://about.me/atodorov) is Difio's founder and lead developer!

For an insight of available updates to you OpenShift applications give
Difio a [try](https://difio-otb.rhcloud.com/applications/mine/)!
