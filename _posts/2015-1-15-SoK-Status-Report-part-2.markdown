---
layout: post
Title: "SoK Status Report part-2"
categories: kde sok
---
Been a while since my last post. Exams came in and threw my momentum off. But now I'm back on track.
I've been working on porting Baloo to use lucene instead of Xapain using [Lucene++](https://github.com/luceneplusplus/LucenePlusPlus).
Lucene++ is a C++ port of the java [Lucene](http://lucene.apache.org/).

The first challenge I faced was adding the lucenePlusPlus library to the project. Which I first solved by adding static paths to the library and include directories. This was the wrong approach as told by my mentor Vishesh Handa, as this would only work on my system. The correct way to do this was to use a cmake finder module for LucenePlusPlus. I'm using one from [here](https://github.com/emjotde/lucenept/blob/master/cmake/FindLucenePlusPlus.cmake).

To use lucene++ a lot of string and other datatype conversions were required between formats Lucene++ uses and their Qt counterparts. (Mainly std::wstring <-> QString) So I decided to write a wrapper to provide clean API's which will be used in my port (using the current Xapian wrapper we have as a reference). I'll be adding more features to this wrapper as I need them going forward. Currently I've ported basicindexingjob in the baloo file component and written a test verify its working, there is a long way yet to go. My working code can be foung in lucene branch of baloo's [git repo](http://quickgit.kde.org/?p=baloo.git&a=shortlog&h=694548c7248eb7e03d963225d54ef78fa12f5602).
