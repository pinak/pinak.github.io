---
layout: post
title: GSoC 2015 - Wrap Up
categories: kde baloo gsoc
---
How time flies by when you're having fun. Still remember the day my GSoC proposal
was selected, like it was yesterday. Now, here we are at the end of the awesome journey.

**So what exactly was my project about?**

My project was titled *"Better Tooling for Baloo"*. So, exactly is Baloo? Baloo
is a framework responsible for file indexing and search for KDE. It is capable
of full text indexing and blazing fast queries, while having a small foot print.
My project involved writting and improving introspection and control tools for Baloo.

This invlolved improving balooctl the already existing commmand line tools to control baloo.
I ended up adding various options to it:

*   *balooctl status* now shows size of the index and state of the indexer i.e. what
    baloo is upto right now.
*   Add option *balooctl status [file..]* which tells if a file is indexed or not
    and if it is not indexed, is it scheduled to be indexed. This option will be
    useful to debug cases in which user cannot find a specific file.
*   Add option *balooctl monitor* which prints out filepaths as they are being indexed.
    Useful for users which want to know what baloo is doing right now.
*   Add option *balooctl index [file..]* which indexes the specified files. Useful
    for indexing specific files manually for eg. in case they might be in an excluded directory.

Now comes the major part of the project *baloo-monitor*, I will explain the it's various
features and challenges I faced while implementing them below.

Baloo Monitor
=============
<center>![](/assets/article_images/gsoc/monitor_final.png) </center>

As can be seen from the screenshot, the application shows the user baloo's current
state, file being indexed, total progress and estimated remaining time and a button to
suspend/resume indexing.

Challenges
----------
There were loads of challenges I had to face to get there. The first one being the
baloo_file_extractor's behaviour which I mentioned in my first post. Once that was
refactored, I had to deal with the internal queue based architecture which was pretty
complex and didn't work well for introspection. So the next step was to come up with
a new architecture which I failed miserably with and finally realizing how hard it is
to design software. Then with loads of help of my mentor, a better architecture was
thought of which is what baloo uses now and works quite well for introspection.

Following this it was a matter of figuring out how Inter-process communication works via
D-Bus and writting the required code for the monitor, which as easy as it sounds now, was
pretty hard for me to get working back then.

Predicting the future is hard. Why do I mention it?
I had to come up with an estimated remaining time algorithm for the monitor.
The only information available to calculate that without insane amount of overhead
was time taken to index past files and files left. Therefore predicting the future.
The problem with this is time taken to index different types of files varies wildly
for instance if we're indexing a complete e-book thingy vs a simple mp3 file, the former
can take more than triple the amount of time.

I tried the simplest approach to begin with, simply average the time taken to index
a single batch till now and multiply it with the number of batches. (we index file in batches).
That didn't work out quite well, because we could have a situation where the bathes in the beginning
were super quick which would drive down the average and the we encounter batches of text heavy files
which would slow down the indexing but wouldn't have enough impact on the average time.

The approach I finally used was to keep track of the time taken to index 5 most recent batches
of files and use that to calculate a weighted average giving the most recent batch
the highest weight. This approach works better than the simple approach as recent batches
have a higher impact on average time but can jump around quite a bit. Still this is the approach
I currently use, maybe in the future I may come up with a better one.

The road ahead
--------------
We've decided that baloo-monitor belongs in KInfoCenter and I am in the process of
making a KCM for it. All in all this was an amazing experience and the three months
that I've learnt the most about various fields of Software Development, from design to
implementation. I am going to continue working with KDE for the foreseeable future :).

Thank you KDE and Google for giving me the chance, and a big thanksto my mentor
Vishesh Handa for dealing with my, sometimes sloppy, code patiently and poniting out
ways to improve.