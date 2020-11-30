---
title: "Thoughts on GitKraken"
author: Shawn
date: "2018-07-19"
categories: [Programming]
tags: [Migrated]
---

So I recently saw the [1.0 release announcement](https://blog.axosoft.com/2016/03/29/axosoft-gitkraken-v1/ "Release v1.0") of Axosoft’s GitKraken. Since I’ve recently been having lots of issues with [Atlassian’s SourceTree](https://www.sourcetreeapp.com/ "SourceTree") for Windows, and have never particularly cared for the UI. I hear that SourceTree on mac is excellent, but I’ve not had the same experience with their Windows client. I’ve also found [Github Desktop](https://desktop.github.com/ "Github Desktop") to be very nice, but a bit limited when it comes to repositories with lots of local branches (not a common use-case on Github repositories, but I encounter it a lot at work.)

I’ve been in the market for a Git client that was as useful and intuitive as [HG Workbench](http://tortoisehg.bitbucket.org/ "HG Workbench") for quite a while now. As a result, when I heard about GitKraken I was eager to give it a try. I’ve been actually quite pleased so far and wanted to share my thoughts on it!

![GitKraken in action](/assets/img/posts/image-not-found.png)

Their advertising is really quite ridiculous.  It almost turned me off to the product at first. But most of it is about how excellent their UX is, and after a few weeks of using it, I actually have to agree.

 

![](/assets/img/posts/image-not-found.png)

DOWNRIGHT LUXURIOUS, AMIRITE GUYS!?

I haven’t used software which pleasantly surprised me by having completely unexpected features that “just worked” in quite a while. The last application I can remember that made me feel like this was Slack. When your product is being favorably compared to Slack, that’s usually a good sign.

There are lots of little nice features such as the convenient, and most importantly – short, first-time demo that takes you around the settings menu to set up Github integration etc. The ability to drag and drop a branch or tag onto another in the source graph to initiate a merge, or the brand-spanking-new-in-v1.1 Fuzzy Search which allows you to search for files, repositories, and branches by text and click a search result to change repos, git checkout the branch, or open a file’s git history.

![](/assets/img/posts/image-not-found.png)

[![](/assets/img/posts/image-not-found.png)

Overall it’s been a really positive experience so far, with just a few bumps in the road. It wasn’t able to detect my global Git merge tool ([Beyond Compare](http://www.scootersoftware.com/ "Beyond Compare by Scooter Software")) for some reason, so for now I still have to run ‘git mergetool’ on the command line during merge conflicts. But their updates so far have been adding nice content and polish, so I’m optimistic that the few minor gripes I have will be remedied soon.

If you’re in the market for a new Git GUI client, I can safely say that GitKraken is by far the best experience I’ve had with one on Windows so far.
