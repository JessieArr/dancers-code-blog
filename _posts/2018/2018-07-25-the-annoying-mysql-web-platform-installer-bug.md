---
title: "The annoying MySQL Web Platform Installer Bug"
date: "2018-07-25"
---

So I recently ran into the following error while installing the second WordPress site on a fresh VM:

The specified password for user account 'root' is not valid, or failed to connect to the database server.

![MySQLError](images/MySQLError2.jpg)

After following a few guides and going through the steps to reset the root password on my MySQL installation and continuing to get the same error, I finally stumbled across the solution in [this blog post.](http://www.swiftsoftwaregroup.com/the-specified-password-for-user-account-root-is-not-valid-or-failed-to-connect-to-the-database-server/ "Swift Software Group")

Since this issue sucked up quite a bit of my time, I figured I’d mirror it on my blog as well. I didn’t need to edit the registry key, simply installing the [MySQL .NET Connector](http://dev.mysql.com/downloads/connector/net/ "MySQL .NET Connector") was enough to fix my issue:

![MySQLFix](images/MySQLFix1.jpg)

Not quite sure why this is needed, but it worked for me. Hope this helps someone else out there!