---
title: "Troubleshooting Steam Matchmaking Servers for Dummies"
author: Shawn
date: "2018-07-25"
categories: [Gaming]
tags: [Migrated]
---

So I recently spent several hours troubleshooting my Space Engineers server, and learned a lot about how Steam does matchmaking while I was at it. I figured I’d make a blog post to share and hopefully save others some time.

First let’s take a look at some pretty pictures that describe how the Steam Matchmaking service works in terms of hosting and joining a game server:

![[gszNOSF]](/assets/img/posts/image-not-found.png)

![[u6HUPdZ]](/assets/img/posts/image-not-found.png)

![[26L7HPY]](/assets/img/posts/image-not-found.png)

It’s not too complex of a process conceptually, but our computers are doing a lot of work in the background to make it happen. So how can we be sure that we’ve set them up properly so that they can do their job?

**Reference: Steam server port information from Valve:** [https://support.steampowered.com/kb_article.php?ref=8571-GLVN-8711](https://support.steampowered.com/kb_article.php?ref=8571-GLVN-8711)

Let’s start from the beginning with items 1 and 2 from the diagram above:

**Can our server identify itself to Steam?**

To be sure that this is working, start the Local/Console server and read what pops up in the console window. It should tell us near the bottom that it connected to Steam.

![[G6r7YRf]](/assets/img/posts/image-not-found.png)

If this fails, then we need to ask ourselves the question: why can my dedicated server not send information **out** to the Steam servers?

We’ll need an internet connection on the machine hosting the server, and our firewall configured properly to allow outbound traffic on the Steam ports in the link above. If you think a firewall may be the problem, turn it off entirely and try to start the game server again.

If it can connect with no firewall running, then turn your firewall back on and do some Google searching to find out how to configure outbound traffic on your firewall software for the Steam ports in the link above.

**Can Steam tell a player about any game server?**

This will cover items 3 and 4 in the above diagram.

The player needs to be able to talk to Steam to ask about the server. This means they will need an internet connection and no pesky firewalls getting in their way. If you fire up your game and can see other people’s hosted games, then this part is working. If not, then your problem is that the game client can’t talk to the Steam matchmaking servers.

Check the internet connection

**Can Steam tell a player about MY game** **server?**

This is the part that burned me. This refers to items 5 and 6 in the diagram. To understand this, you need to know a little about networking. Routers and firewalls are very generous when allowing traffic from a computer to go elsewhere, AND when allowing responses back from the server you just contacted. They assume the connection is a response to a request you just made and allow it through.

However when another server tries to connect to your router/server without you having made a request from them first, by default your router and firewall will treat the unsolicited connection like an intruder: denied!

To check if this is the problem, use the Steam Server Browser built into the Steam client to see if you can connect to your server and find information about the game. If not, then Steam won’t be able to tell Space Engineers players about your game either. In the Steam client go to View > Servers, then select Favorites, “Add a Server” and enter your server’s IP/domain name and optionally port. Then click “Find games at this address…”

For people hosting their servers at home, go here ([http://www.whatismyip.com/](http://www.whatismyip.com/)) to find your public IP. This will be different from your computer’s IP address if you use a router. Routers set up a local network for you and give out local IP addresses to the computers on them.

If your server is communicating with Steam correctly, you should see information about your games:

![[Cdaoc6Y]](/assets/img/posts/image-not-found.png)

So if you want Steam to be able to make an unsolicited connection to your server to scan the 30 Steam matchmaking ports, and then tell players what it found, your router and firewall need to allow **inbound** traffic on ports 27000 – 27030 (or possibly just the one port you’re actually hosting the game on.)

How to do this will vary based on your setup, but routers will need port forwarding turned on, allowing unsolicited connections to your router on the game’s port to be forwarded to your computer instead of rejected. If you host your own web server, routers won’t be a concern, but both public web servers and home computers will need their firewall to allow inbound connections on the Steam ports for this to work. A Google search for your router/firewall should teach you how to do this.

Items 7-9 should work well if you’ve gotten this far. Your client can talk to Steam, your server can talk to Steam, and Steam can scan ports on your server. All that’s left is Steam Groups!

**Is the player allowed to join based on their Steam Group ID?** To find out your Steam Group ID, use this link, but put your Steam group name in the URL. The ugly XML you see will include the group’s full ID near the top of the page.

http://steamcommunity.com/groups/\[groupname here\]/memberslistxml/?xml=1

Once you have your Steam group ID, you can add it to your server information:

![[bxkhugz]](/assets/img/posts/image-not-found.png)

0 will allow all connections. If you change the group ID field to something other than 0, then only Steam players in the designated group will be allowed to join. To test this, the Space Engineers game client can show us a list that is **not** filtered to exclude games which won’t allow you to join based on your group. Simply unckeck the ‘Allowed Groups’ box to see the full list of all servers:

![[XJYuKaG]](/assets/img/posts/image-not-found.png)

And that’s about all I know about Steam matchmaking and troubleshooting Space Engineers dedicated servers. I hope this helps some folks out there!
