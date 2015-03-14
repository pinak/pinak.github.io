---
layout: post
Title: "SoK conclusion"
categories: kde sok
---
My SoK journey has come to an end. It was the best learning experience ever. As the say no better way to learn than to get your hands dirty. My project, even though it was more oriented towards research, gave me hands on experience with Baloo's codebase. Looking for a better alternative to Xapian, which is after all a core part of Baloo, is no small task.

What I acomplished:
-------------------

1. Read the code for current implementation which uses the Xapian backend and figured out why it falls short for our use case. Compiled a list with Vishesh Handa [Xapaian Problems](http://community.kde.org/Baloo/XapianProblems).
2. Read Lucene's documentation and and implemented a proof of concept port of Baloo using Lucene. The code can be found [here](http://quickgit.kde.org/?p=baloo.git&a=shortlog&h=872931312156a49bcf8da76d702cefc754607952).

Outcome:
--------

We will be benchmarking the various backends (Xapian, Lucene++, custom backend - more on that later) once I iron out some minor kinks with the lucene port. While working with Lucene I realized it is plagued with some of the same problems as Xapian, namely relies on exceptions, concurrency etc. Also one of the main reason that prevents us from using Lucene is that there is no properly maintained C++ port. For my project I worked with Lucene++ which lags behind the JAVA Lucene by a major Version.(Lucene++ is 3.0.x and JAVA lucene is at 4.10.x) and the developer has no plans in catching up. So it is very unlikely we will use Lucene++ in Baloo.

What Lies Ahead:
----------------

Vishesh Handa is working on a custom solution for replacing Xapian and it is looking very promising. Now that I have gotten really familiar with Baloo's architecture maybe I can help around with that. Also I will continue contributing to KDE projects. A shout out to the wonderful KDE community which has, along with giving me an awesome Desktop Environment, has given me the power and knowledge to contribute back and help in shaping its future. Also a big thanks to my mentor Vishesh Handa who was always there to help me when I got stuck.
