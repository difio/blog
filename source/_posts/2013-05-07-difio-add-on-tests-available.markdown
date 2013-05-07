---
layout: post
title: "Difio Add-On Tests Are Available"
date: 2013-05-07 15:03
comments: true
categories: ['News']
---

Today [Difio](http://www.dif.io) is pleased to announce the general
availability of [add-on tests](http://www.dif.io/add-on/) which are
designed to test and verify potential issues or
known bugs. Add-on tests are provided as a
[subscription service](https://difio-otb.rhcloud.com/profiles/mine/)
for 10 $ per month. First month is free.

What add-on tests are available
-------------------------------

* **API diff** - Difio generates API definition from the package
source code. Changes in API could be
backward incompatible and result in application crash and runtime failures.
API diff is currently available for **Python**, **PHP** and **Java**.

* **Full diff** - this is the full git diff between two package versions.
It is available for informational purposes.

* **Package Size Change** - packages that change their size significantly
can be a sign of
a [corrupted build](https://github.com/tschellenbach/Django-facebook/issues/262).
This test reports any size changes over 30%.
See [DIFIO-12243](http://www.dif.io/updates/django-facebook-4.2.11/django-facebook-4.3.0/12243/) for example.

* **File Size Change** - inspects files which are present in both versions.
Any size change that is both more than 20% and more than 20 KB or
any file that changes from being zero-sized to non-zero sized, and vice-versa is reported.

* **Added non-text Files** - new files are classified with libmagic.
Any non-text file is reported.
Bugs like [Django #19858](https://code.djangoproject.com/ticket/19858) can
be found with this test. For example see [DIFIO-12987](http://www.dif.io/updates/Django-1.4.3/Django-1.4.4/12987/).

* **Modified Files** - lists all modified files. You should manually review the
list and inspect if unwanted files were modified.

* **Added Files** - lists all newly added files. New files are usually resources, tests of new
functionality. Manually inspect to verify additions are expected.

* **Removed Files** - files in packages should be removed only if properly obsoleted or
initial inclusion was a bug. Removing modules or parts of them can break the API.

* **Renamed Files** - renaming files can break API. This test lists all renames
between two versions.

* **Permissions Change** - file permissions change (Linux/UNIX only) could indicate
security issues. In a source package without executable programs permissions should
not change.

* **Symlinks** - this test traverses the entire package tree and reports any symlinks found.
It will report FAIL if any symlinks exist in the new package.
For example see [DIFIO-16005](http://www.dif.io/updates/factory_boy-1.2.0/factory_boy-2.0.0/16005/).

* **File Types Change** - this test compares file types reported by libmagic between
two package versions. Files should not be changing their type between updates.

* **Virus Scan** - a virus scan is performed on the package using the ClamAV virus scanner.
Even though it is unlikely that packages contain viruses, it's still important to know if anti
virus tools will trigger false positives.

* **Test Cases** - this test reports any changes in test cases. It counts the number of available
test case files in some well known locations. If new version is missing tests or has less
then severity will be VERIFY or FAIL.


---

Difio is constantly working on improving the service. In the mean time
[start following packages](https://difio-otb.rhcloud.com/dashboard/follow/),
invite your friends and send us your feedback via
[GitHub](https://github.com/difio/bugs/issues/new)
or [Twitter](https://twitter.com/DifioNews).

