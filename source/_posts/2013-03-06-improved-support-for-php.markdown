---
layout: post
title: "Improved Support for PHP"
date: 2013-03-06 11:05
comments: true
categories: ['News']
---

Today [Difio](http://www.dif.io) is pleased to announce improved support
for the PHP programming language and the 
[Composer](http://getcomposer.org) dependency management tool.

Previously only PHP PEAR packages were supported and it was not possible
to manually import a list of packages. Starting today, these issues have been
fixed.

At the moment Difio supports three upstream sources for PHP packages:

* <https://packagist.org/>
* <http://pear.php.net/>
* <http://pear2.php.net/>

Users are now able to manually import package list from their PHP applications
using Composer.

To register PHP apps go to
<https://difio-otb.rhcloud.com/application/import/composer-show/?>
and paste the output of `php composer.phar show --installed` command.

For example:

    $ ./composer.phar show --installed
    doctrine/common                              2.3.0   Common Library for Doctrine projects
    imagine/Imagine                              v0.4.1  Image processing for PHP 5.3
    pear-pear.php.net/HTTP_Request2              2.1.1   PHP5 rewrite of HTTP_Request package ...
    pear-pear.php.net/XML_Util                   1.2.1   Selection of methods that are often needed when working with XML documents ...
    pear-pear2.php.net/PEAR2_Cache_SHM           0.1.0   Allows you to share data across requests as long as the PHP process is running. ...
    pear-pear2.php.net/PEAR2_Text_Markdown       0.1.0   This is a port of Solar_Markdown.
    psr/log                                      1.0.0   Common interface for logging libraries
    symfony/symfony                              v2.2.0  The Symfony PHP framework
    twig/twig                                    v1.12.2 Twig, the flexible, fast, and secure template language for PHP

This application contains packages from the three different sources and they
will be properly parsed and recognized by Difio.

What's next
-----------

Difio is constantly working on improving the service. We are now looking into
API diff support for PHP among other things, so stay tuned!
In the mean time
[start following packages](https://difio-otb.rhcloud.com/dashboard/follow/),
invite your friends and send us your feedback via
[GitHub](https://github.com/difio/bugs/issues/new)
or [Twitter](https://twitter.com/DifioNews).
