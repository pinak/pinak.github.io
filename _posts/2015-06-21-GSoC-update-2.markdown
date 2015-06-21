---
layout: post
title: GSoC 2015 - update 2
categories: kde gsoc baloo
---
It has been a while since my last post, been busy working on my project :p. I must say it has been
a great learning experience. With the refactoring done as mentioned in my previous post
I began working on CLI tools baloo currently provides, we currently have a tool called balooctl
which has loads of options to control baloo. I added 2 more options to the existing set

* *balooctl status* [file..] it tells us about the status of the specified files i.e. if they are indexed
or not and what level i.e. the basic indexing and content indexing.
* *balooctl index* [file..] this option can be used to index the specified files manually.

Then I started working with the first major part of my project that is the Monitor. So I began by exporting URL of
every file we start indexing over D-Bus after eventually figuring out how D-Bus works.
Then I made a simple CLI utility which which on running prints out url of each file as it is indexed.
This utility has been merged in the master branch and can be used by calling *balooctl monitor*.

Now on to the fun part working with a UI for the monitor, I decided to go with qml for the UI mainly because
of my familiarity with it (or rather my "unfamiliarity" with QWidgets) and my love for shiny new stuff. I understand that
there is a performance penalty by using qml but for now the application seems to be running without any perceivable
slowdowns, but it is pretty basic as of now, we'll see how it goes. Here's the screenshot of the monitor in action.

<center>![](/assets/article_images/gsoc/monitor.png) </center>

For those of you who want to give it a shot, it has been merged in baloo's master branch so if you build and
install baloo from master you'll get an application "Baloo Monitor", it is pretty basic for now.


I'm working an a time estimation logic which will try and not keep the user in the dark as to how much more time the indexing
will take it hasn't been added to the monitor yet. Estimating time **accurately** is a bigger challenge than I initially
anticipated. This is mainly because the varied nature of files on an average computer. Indexing a most of the stuff is almost instantaneous whereas time taken to
index the pdf's or other text heavy stuff largely depends on the amount of text in it, as we index it's content too.
Simply relying on the average time it takes to index a fixed number of files, which is the current state, somewhat
works but results in jumpy and sometimes inaccurate results. So time estimation needs refinement.
So in the coming weeks I'll be working on:

* Cleaning up the D-bus code (using D-bus interfaces with proper XML descriptions)
* Adding more features to the monitor
* Refining time estimation
