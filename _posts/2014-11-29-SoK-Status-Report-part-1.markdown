---
layout: post
title: "SoK Status Report part-1"
categories: kde sok
---
As mentioned in my previous post I'd be writing about my journey through SoK in
upcoming posts, here I am with my first status report.

So far what I've learnt/done:
-   Skimmed through xapian's 'getting started' Documentation to get familiar with the basics
    of xapian.
-   Analyzed baloo's code to know how and why are we using xapian.
-   Then I implemented a small program using xapian to add index and search. I did this
    to get familiar the basic API's. The code can be found in my [scratch repository](http://quickgit.kde.org/?p=scratch%2Fpinakahuja%2Fbaloo-sok.git)

*Note: It is necessary to explain what an xapian document is before proceeding further. I'll try my best to keep it breif.
Xapian Document is the basic unit returned by xapian after a search. The implementation in baloo is: every indexed file has an associated document which contains the terms relevant to the file. This is stored in xapian's database and mapped to the file using and SQLite database.*

-   Got familiar with xapian-inspect, which is a tool used to inspect contents of an xapian database table. I used this for inspecting tables of the database created by the basic utility I made to understand how an xapian database is organized internally. The main tables in the database are:
    -   **Posting list table**: This maps the indexed terms to the documents in which they occur. This is the main table
        that used in resolving queries.
    -   **Record able**: This stores the data associated with a document.
    -   **Term list table**: This table maps the documents to the to the terms that occur in the document.
    -   **Position table**: This table maps document + term to the position in the document. This information
        required for phrase queries.
-   Started looking for problems with xapian in accordance to our use case. I've made a [wiki
    page](https://community.kde.org/Baloo/XapianProblems) for a list. The problems that I've currently figured out are:

    -   It heavily relies on exceptions. Exceptions are not well supported in Qt and might make the application crash as mentioned [here](http://qt-project.org/doc/qt-5/exceptionsafety.html). For example while locking  a database Xapian expects the program to catch certain exceptions and retry if they are caught.

    -   If we want to read and write to an Xapian database simultaneously we need to keep separate copies for reading and writing, thus wasting memory.

    -   It does not handle data that is changing frequently, if data in document changes to frequently it can lead to a conditions in which locking the database for writing becomes impossible thus making baloo fail.

    -   Baloo needs support for normalizing text i.e. removing all diacritic marks and also needs to split words with '_' to generate terms, Xapian's term generator doesn't provide support for either. So baloo uses its own term generator.

    -   While searching for something the user may not type complete words so we need to look for every possible expansion of the words in a query,  xapian doesn't provide this feature so we're using our own query parser.

This list is not exhaustive and I'll be adding more problems as I figure them out so keep a look out on the wiki page.
Once again a big thanks to my mentor Vishesh Handa who guided me through all this.
