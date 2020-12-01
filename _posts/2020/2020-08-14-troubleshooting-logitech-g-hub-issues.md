---
title: "Troubleshooting Logitech G Hub Issues"
author: Shawn
date: 2020-08-14 12:00:00 -0600
categories: [Tech]
tags: [Logitech, Gaming]
---

Logitech has a long-standing tradition of making really quality hardware that is completely let down by their terrible software, and the new G Hub and the headsets that depend on it are no exception.

Recently, a G Hub update failed for me, resulting in the application becoming unusable. It did so while my headset was muted, and you can't unmute the headset using the button on the headset without the G Hub software. Ughhhh.

So I uninstalled G Hub and tried a fresh install, but... my computer froze. I restarted and tried again, and it froze during the installation again. Here we go.

To make matters worse, both uninstalling and a failed installation do _not_ clean up all of the G Hub files on disk, so you will have junk hanging around from previous installations that can trip up a new install.

### How To Fix It:

First things first, Logitech has a [troubleshooting page](https://support.logi.com/hc/en-us/articles/360023192454-G-HUB-Install-Uninstall-Update-Troubleshooting) in their knowledgebase with some troubleshooting steps. Those seem to fix the issue for most people, but didn't for me - we'll get to that later. The gist of the steps is:

#### Stop LGHUB and All of its Friends

Run Task Manager (ctrl + shift + Esc) and kill any of the following programs if they're running: "LGHUB.exe", "LGHUB Agent.exe", and "LGHUB Updater.exe"

#### Clean Up the Application Data

Delete the LGHUB folders in the following two locations:

- Your Roaming AppData folder: (Press Windows + E to open an explorer window, then type %appdata% into the search bar. Or go to C:\\Users\\\[YourUsername\]\\AppData\\Roaming)
- Your Program Files folder: (Windows + E to open an explorer window, then type %programfiles% into the search bar. Or go to C:\\Program Files)

Once this is done, some users report success. But others have claimed that they needed to delete the LGHUB Uninstall record from their registry. To edit your registry:

- Press the Windows key, then type "regedit" and open the Registry Editor.
- In the path bar at the top, enter the following path: "Computer\\HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Uninstall"
- Find the LGHUB record in Uninstall. For me it was named {521C89BE-637F-4274-A840-BAAF7460C2B2} You can check the "DisplayName" property to be sure - it should say "Logitech G HUB"
- Delete the Registry entry.

![G Hub Registry Entry](/content/2020/registry.png)

#### Restart Windows

Windows likes to be restarted. It's just a thing. I'm not sure whether this is required, but it can't hurt.

#### Reinstalling the Blessed Download

Some users report that the latest version of the LGHUB installer doesn't work for them, and that they were able to work around the issue by downloading an older version. You can view many of Logitech's downloader releases on their FTP page here: [ftp://ftp.logitech.com/pub/techsupport/gaming/](ftp://ftp.logitech.com/pub/techsupport/gaming/).

Some users have said that "lghub_installer_2018.7.2535.exe" did it for them, others have said that "lghub_installer_2018.9.2778.exe" was the magic sauce. I'll leave that to you to determine.

#### The Install Still Hangs!

Even with all of this handholding, the installs were still freezing my computer. What finally got it working for me was remembering a very old forum post about a similar issue in the predecessor to the G Hub: the Logitech Gaming Software. That software also caused my computer to freeze during installation, and a user reported an absolutely unbelievable workaround: they unplugged the SATA cable from their computer's DVD drive. I tried that and, to my astonishment, it worked for the LGS.

After several hours of troubleshooting, I remembered this old workaround from about 4 years ago and decided to try it for the new G Hub software. And it worked! The software actually installed.

I have no idea what sort of shenanigans they're doing in the code for these plugins that can cause "having a DVD drive plugged in" to freeze your computer, but it appears to be what's happening in some cases.

#### Update to the Latest Version

Once you've done all of this and gotten it running, navigate to the G Hub Settings and check for updates.

![G Hub Settings](/content/2020/g-hub-settings.png)

![G Hub Updates](/content/2020/g-hub-updates.png)

This took a while for me, and eventually led to me having to restart my computer twice - once for the G Hub update, and once to install the drivers to my headset, because Logitech doesn't know how to write good software. But after that I was up and running.

#### My Hardware Isn't Detected!

This happened to me, but was eventually resolved by just updating the G Hub. If that doesn't work for you, though, there is a Logitech forum post that provides [troubleshooting steps](https://support.logi.com/hc/en-001/community/posts/360034109093/comments/360008882853) for this issue. I'll include them below:

> If your G PRO X is not being detected, Please follow these steps: 
> 
> • Go to device manager → click on " View " tab then choose show hidden devices → Go to " Sound, Video and Game controllers " → Your headset should appear as "Logitech PRO X Gaming Headset" and the Driver Provider should be Logitech with a Driver Date of 7/2019. 
>
> • If not Go to device manager → click on " View " tab then choose show hidden devices → Go to " Sound, Video and Game controllers " → Right-click Properties → Driver tab → Update Driver → Browse my computer for driver software → <X>:\\ProgramData\\LGHUB\\depots\\<select the latest build>\\driver_audio.

They also mention that if this doesn't work, you can reinstall the G Hub software and try reinstalling it again. In that cause, I guess just scroll to the top of this blog and start over, with my condolences.

#### Conclusion

Logitech makes really quality headset hardware, but their software has been a complete dumpster fire for as long as I've been buying from them. If there's any other headsets out there that include macro keys on the headset, _please_ let me know in the comments because I am beyond ready to stop buying from Logitech, but having a push-to-talk key on a wireless headset is a feature I really don't want to live without.

And in case anyone from Logitech happens to be reading this: your software doesn't need to have Discord and Overwolf integrations, game thumbnails for the hottest games, ways for third party apps to change the light settings, and all this other fancy stuff that hardly gets used.

It just needs to work. Reliably. Every time. When users go to your [forums](https://support.logi.com/hc/en-us/community/topics) or [Reddit](https://www.reddit.com/r/LogitechG/) they shouldn't see post after post of users having the same issues literally just getting their gaming devices to work going back for years. You make good hardware, that alone will earn you loyal customers, if the software doesn't constantly sabotage it. Fix your development and QA practices, please.
