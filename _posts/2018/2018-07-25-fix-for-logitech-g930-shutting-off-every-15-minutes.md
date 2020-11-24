---
title: "Fix for Logitech G930 Shutting Off Every 15 minutes"
date: "2018-07-25"
---

Not too long ago I shopped around for a wireless headset which had surround surround support, and eventually settled on the [Logitech G930 Headset](http://www.amazon.com/gp/product/B003VANOFY/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B003VANOFY&linkCode=as2&tag=danscod07-20&linkId=GWSRFWBFHMSUZJPA "Logitech G930 headset").

While the hardware is excellent, and the sound is quite good, sadly the software designed to support the surround sound, macro keys, and showing the battery status is the Logitech’s [Gaming Software](http://support.logitech.com/en_gb/software/lgs "Logitech Gaming Software") suite, aka LGS. I have never used this software with any of their other products, so I can’t comment on its overall quality, but its support for the G930 headset is really quite awful.

Google’s [search results](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=g930+problem "Logitech Search") are littered with people complaining about various issues with the headset’s drivers and the gaming software, some of which are quite severe. Logitech also doesn’t seem very interested in solving any of the driver/software problems for this headset, as some of the simpler issues have been open on their support forums for 5+ years without a patch being released.

It’s really a shame because the hardware itself is quite good, and it is the only headset I’ve managed to find which is: wireless, supports surround sound, and also has macro keys on the headset (useful for push-to-talk and skipping songs while I’m in the other room.)

One particularly annoying problem many people seem to have is that, while the headset works just fine out of the box, as soon as they install the Logitech Gaming Software, it begins to [turn itself off every 15 minutes!](https://forums.logitech.com/t5/Logitech-G-Headsets/G930-headset-auto-shut-off/td-p/504096 "Logitech Support Forums") This happened to me as well, and it turns out that it is just a default power-saving setting in the XML config used by LGS to determine how it should manage the headset. Since it’s a config file you’d think that you could just change the headset’s settings in LGS – no such luck. LGS provides no way in the UI to update this setting, requiring you to find and modify the XML file manually, or just get used to it shutting off every 15 minutes.

With the default install location, the file is located at the following path: C:\\Program Files\\Logitech Gaming Software\\Resources\\G930\\Manifest\\Device\_Manifest.xml

You can simply change the value in the <battery> node’s turnOffInterval attribute to “0” to disable this battery saving feature entirely.

This is well and good, but I always forget the path when I reinstall the software on a new machine, and don’t feel that this is very intuitive for people who aren’t comfortable editing XML config files manually.

So tonight I wrote a simple Windows application to help users modify the battery configuration settings which are not normally editable through LGS and uploaded it to [Github](https://github.com/JessieArr/LogitechG930Fix "https://github.com/JessieArr/LogitechG930Fix").

If you are experiencing this issue with your G930, I hope either this blog or my application helps. And if you are a programmer who wants to make an improvement and submit a pull request, feel free to do so!
