---
layout: post
title: "Toolbox #006: CleanADGroupMembers"
tag: [PowerShell, Toolbox, AD]
published: true
---
Synopsis: A PowerShell script to clean out AD groups from disabled user accounts.

In a previous [post](https://www.cloudsparkle.be/2020-09-14-CountCTXAppUsers/), I briefly mentioned you should use AD groups for publishing Citrix applications. I think it's safe to say this goes for any EUC technology out there.

Whatever the use case, keeping your AD groups clean and clutter-free can be a challenge. I mean: it simply is a challenge. In particular, the presence of disabled AD user accounts. Removing them from a single AD group is relatively easy, using the builtin PowerShell cmdlets. In the real world out there, things are different.   

There's group nesting for one. Would you like to have those child groups cleaned as well? It depends... as always. There are use cases for both options, I guess.  

When you do want to clean them all, that's where things get tricky. Yes, native PowerShell cmdlets do support gathering members recursively from any AD Group. However, you only get the users, not the child group they belong too. That reference is not there, which makes cleaning impossible for obvious reasons.

So I wrote my own function to check the group recursively. I did also make this recursive part optional. In other words, you will be asked if you want to go all the way or not.

And to wrap up, by default, the script generates a CSV file with disabled accounts and the AD group they have been removed from. You know, to keep a record of things.

As always, you can find these scripts on my GitHub Repo [here](https://github.com/Cloudsparkle/CleandADGroupMembers).
