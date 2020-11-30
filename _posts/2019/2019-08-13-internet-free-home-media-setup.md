---
title: "Internet-Free Home Media Setup"
author: Shawn
date: "2019-08-13"
categories: [PLEX]
tags: [Migrated]
---

So recently COX Communications has decided to just have a 3-day internet outage because they're awful. As a result, I was quite glad that I have spent a fair bit of time digitizing my DVD collection and organizing it all on a home PLEX server on my local network, so I decided to settle in for a movie marathon until the internet was restored.

![Lakeside Campfire with Relaxing Nature Night Sounds (HD ...](https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fi.ytimg.com%2Fvi%2FNUKKzdVy0EI%2Fmaxresdefault.jpg&f=1)

Buuut it turns out that my PLEX server running on my NVidia Shield wouldn't let me connect to it without phoning home over the internet to the PLEX website. Awesome.

So then I decided to give Kodi a try, but their app is awful and although I was able to get it to stream media from my NAS on Windows, it simply wouldn't work on Android.

At this point I did some research and figured out a solution that is working (internet's still out, by the way - I'm writing this on my phone) and figured I'd share it.

## Enter DLNA

After some research, I found out that [DLNA](https://en.wikipedia.org/wiki/Digital_Living_Network_Alliance) (Digital Living Network Alliance) is a standard designed for sharing streaming media content - including on the same home network via [UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play). What's more, it is supported by PLEX but is disabled by default. So you simply need to [turn it on](https://support.plex.tv/articles/200350536-dlna/) once you have your PLEX server set up (I already did - setup is easy if you have internet.)

![chrome_2019-08-13_00-43-45](images/chrome_2019-08-13_00-43-45.jpg)

![chrome_2019-08-13_00-45-30](images/chrome_2019-08-13_00-45-30.jpg)

Once this is done, PLEX will begin broadcasting its availability via DLNA on your home network, and devices on the same network which support UPnP can discover it automatically.

## Now How Do We Watch It?

The PLEX viewer is great, but it's primarily designed assuming you will have internet access. Having to tether two devices to my phone just so they can hit the open internet to log in and discover that they've been 5 feet apart this whole time is a pain, and you'll have to do it for every device, not to mention remembering and typing your login on each one. Not an ideal experience.

So I decided to ditch the PLEX viewer entirely and discovered that [VLC Media Player](https://www.videolan.org/vlc/) supports UPnP. Not only this, but they have nice Android and iOS apps as well. On Windows the setup is trivial: simply open the Playlist view and select Universal Plug'n'Play:

![vlc_2019-08-13_00-52-50](images/vlc_2019-08-13_00-52-50.jpg)

Once this is done, you should see your PLEX server in the list of DLNA devices broadcasting on your network. Select it, and then you will be able to browse its contents in a folder-like structure.

## What About Mobile Devices?

I've been using VLC's Android app which seems very nice. But there's one big gotcha: for me I couldn't detect any DLNA content on my home network while connected to my mobile data network. I guess it sends all of your traffic to your mobile network rather than wifi when the wifi doesn't have internet. Normally this is convenient, but in this case we _want_ to send our traffic locally.

To turn off mobile data on Android, go to Settings > Network & Internet > Mobile Network > Mobile Data > Off. Now the only network we're connected to is the Wifi that our PLEX servers is broadcasting our DLNA content on, and VLC should find it no problem.

Simply open VLC, then in settings select "Local Network"

![ApplicationFrameHost_2019-08-13_01-00-09](images/applicationframehost_2019-08-13_01-00-09.jpg)

Then after VLC searches your local network, you should see your PLEX server as one of the results:

![ApplicationFrameHost_2019-08-13_01-04-27](images/applicationframehost_2019-08-13_01-04-27.jpg)

Now select your server and you should be able to browse your media via the virtual folders.

* * *

It took a surprisingly particular setup to really get what I want, but I'm now quite happy with my home media setup. There's lots of DLNA servers and viewer apps out there, but for me, the duo of PLEX and VLC ended up being the simplest of quite a few setups I tried.

Hopefully if you're looking for a very simple, offline-friendly media server setup for sharing your own media over your local network with several devices, this may be just what you're looking for!

Now I'm gonna go marathon movies while I wait for COX Communications to stop being a disgrace and restore my internet...
