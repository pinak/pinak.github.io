---
layout: post
title: GSoC with KDE
categories: kde gsoc baloo
image: /assets/article_images/gsoc-intro/gsoc_logo.jpg
---
Guess whose GSoC project proposal got accepted? I am so excited, to tell you all that I'll be working on Baloo along with amazingly experienced KDE developers, this summer, getting to learn loads of stuff and be paid for it! Most importantly I'll also get a Google Summer of code T-Shirt :) , can't think of a better way to be spending my summers. Thank you KDE for giving me this chance,and a big thanks to Vishesh Handa for all his guidance and feedback on my proposal.

My project
----------
So, my project is titled: **Better Tooling for Baloo**. Let me begin by explaining what Baloo is. According to its wiki page it is *"Baloo is a metadata and search framework by KDE."* What exactly does it mean? Baloo is responsible for providing *full text search* capabilities to KDE applications. It doesn't end there it also provides searching on basis of metadata of various types of files. To acomplish this it indexes file contents and metadata using various plugins ,called *extractors*, to handle different types of files. It then exposes the data it has indexed with the help of various API's. So thats a very high level view of how it works. Now, my project, as the title states will provide better tools for Baloo. These tools will mainly be:

1. A UI (and some CLI tools too) to control and monitor Baloo's progress and current status. This will give power users more control over Baloo and also make debugging erratic behaviour much easier. The UI will be something along these lines:
<center>![Monitor Mockup](/assets/article_images/gsoc-intro/monitor_mockup.png)</center>
there will be certain advanced features like logging, which will keep track of which files have been indexed, how much time it took to index the file and which files, if any, made the extractor crash.
2. A tool to visualize which types of files take up how much space in the system currently. This will be most likely a pie chart which would look like:
<center>![Space Visualization Mockup](/assets/article_images/gsoc-intro/pie_mockup.png)

These designs are simply mockups that I made for my proposal. They will be improved with feedback from KDE's Visual Design Group and the community.

There's a long road ahead and loads of stuff to be learnt, awesome code to write! Looking forward to it.

For those of you interested in more details about my project here's a link to my proposal: [Google Drive](https://drive.google.com/file/d/0BxyaYrqdfxSOYnNVUm9jNHVNWU0/view?usp=sharing)
