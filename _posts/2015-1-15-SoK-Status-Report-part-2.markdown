---
layout: post
Title: "SoK Status Report part-2"
categories: kde sok
---
Been a while since my last post. Exams came in and threw my momentum off. But now I'm back on track.
I've been working on porting Baloo to use lucene instead of Xapain using [Lucene++](https://github.com/luceneplusplus/LucenePlusPlus).
Lucene++ is a C++ port of the java [Lucene](http://lucene.apache.org/).

The first challenge I faced was adding the lucenePlusPlus library to the project. Which I first solved by adding static paths to the library and include directories. This was the wrong approach as told by my mentor Vishesh Handa, as this would only work on my system. The correct way to do this was to use a cmake finder module for LucenePlusPlus. I'm using one from [here](https://github.com/emjotde/lucenept/blob/master/cmake/FindLucenePlusPlus.cmake).

To use lucene++ a lot of string and other datatype conversions were required between formats Lucene++ uses and their Qt counterparts. (Mainly std::wstring <-> QString) So I decided to write a wrapper to provide clean API's which will be used in my port (using the current Xapian wrapper we have as a reference). I'll be adding more features to this wrapper as I need them going forward. Currently I've ported basicindexingjob in the baloo file component and written a test verify its working, there is a long way yet to go. My working code can be found in lucene branch of baloo's [git repo](http://quickgit.kde.org/?p=baloo.git&a=shortlog&h=694548c7248eb7e03d963225d54ef78fa12f5602).

Edit (19th January 2015):

As Kais Hassan mentions that I should probably add an explanation as to how lucene can be utilized by baloo which is primarily
a desktop searching solution, here It is:
Baloo requires full text indexing and searching capabilities, for which we currently use xapian, but there are some problems with it as I previously stated in my [Status report 1](http://pinak.github.io/kde/sok/2014/11/29/SoK-Status-Report-part-1.html).


Lucene, which is primarily used for internet search solutions, can easily be used for desktop searching suites.
It uses documents which are the basic unit for searching and indexing. A document consists of Terms which simply map
Field -> value. Queries retrieve documents which contain the specified value for a field (Queries can be more complex
though and involve many fields). We create a document for every file, when we index the files.
These documents contain appropriate values (URL, name, type, content etc) for the file.
