---
layout: post
title: "Graphical or Tabular View? You Vote, We Code"
date: 2013-01-24 14:43
comments: true
categories: ['ideas', 'polls']
---

Hello guys! We haven't posted in a while and we're sorry for this. Here's an idea which is
going around in our heads. Let us know what do you think. 

Tabular View
-------------

Currently when you log into the [application dashboard](https://difio-otb.rhcloud.com/applications/mine/)
and navigate to the details view of each application you see this:

![Tabular view](/images/appdetails.png "Tabular view")


The installed packages are on the left while new versions are on the right. The links point to
more detailed information about changes between the two versions. By default only the
available updates are shown but you can display all installed packages as well.


We also have a history page which holds a snapshot of your installed depednencies
whenever they change. It looks like this:

![History records](/images/history_records.png "History records")


These two pages inform you about the latest and greatest versions
and which ones you have been using in the past. However they don't show you
any version release history nor how does your application relate to that.


Graphical View
--------------

Our proposal is to implement a graphical view as shown on the mockup below:

![Graphical view](/images/app_graph.png "Graphical view")


On the verical axis are all the dependencies used by your application. By default only outdated
ones are shown, sorted by their name for readability.

On the horizontal axis are all available versions for that particular package shown as markers.
A tooltip shows you the package name and version. Density and scale is based on release dates.
Zoom will help you investigate more closely.

The marker or the tooltip can be a link to the standard page where these two versions are compared and analyzed.
The marker icon can be left as is or be one of the icons representing Low, Medium or High change rate.

Individual packages can be turned on or off of course.


Application state is shown as a line connecting the versions you have installed. Previous states, where dependency
versions were different can be represented as similar lines on the left. The leftmost being the oldest history record.
State lines can also be turned on or off if the view gets too crowded.


You Vote, We Code
-----------------

The ball is yours now! If this page gets over 50 tweets, comments, shares or likes we are going to implement this in [Difio](http://www.dif.io).
A breakdown of features will be posted in the comments below. You can vote up or down for any of them. 

If you have any other ideas or suggestions please let us know. You can use the comments form or submit them
via [GitHub](https://github.com/difio/bugs/issues/new) or [Twitter](https://twitter.com/DifioNews).






