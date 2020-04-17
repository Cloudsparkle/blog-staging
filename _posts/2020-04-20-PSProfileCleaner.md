---
layout: post
title: "Toolbox #003: PSProfileCleander"
tag: [PowerShell, Toolbox]
published: true
---
Synopsis: A PowerShell script to clean up those local profiles.

User profiles are as old as Windows itself. With every Windows version, something tends to change.
Not always for the better, but that's a discussion for another time.
There are several profile types, but for this post, the type doesn't matter all that much.

Some of you may remember a tool called UPHCLEAN.  
Some of you may remember DELPROF.EXE, or its more "modern" variant: DELPROF2.EXE.  
All those tools share a common goal: delete user profiles.

##### Why do we need a tool to delete user profiles?

In a XenApp/CVAD/RDSH environment, user profiles just don't always behave themselves. When a user logs off, their user profile needs to go as well, and there's no point in sticking around.
The biggest issue is when they are in doubt. Meaning, the user profile wants to leave, but not just yet. In other words, when some part of the user profile is left behind, the real trouble starts.

So a while ago I ran into exactly that problem. User profiles remained partially behind on servers after users had logged off.
I could have solved this in a number of ways, probably, but I wanted to give my new best friend PowerShell a shot at it.

So I wrote PSProfileCleaner, a script that deletes user profiles that are not in use, not excluded, and not special. Special, you say? Yes, things like the Default Profile and other "system profiles" don't like to be deleted. You may also have a case for Administrator accounts, service accounts, … that are better of left alone. Those you can specify as exclusions in my script.   

All other profiles, when not loaded (as in that user is working on the system), get deleted. All those deletions get logged in a log file at the location of your choice.

By default, the script runs in a loop continuously. There is a possibility to have just one go at it, using a RunOnce parameter.
As always, you can find this script on my GitHub Repo [here](https://github.com/Cloudsparkle/PSProfileCleaner).
