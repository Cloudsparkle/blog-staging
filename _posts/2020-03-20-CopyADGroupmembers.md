---
layout: post
title: "Toolbox: CopyADGroupMembers"
image: /img/powershell2.png
tag: Powershell, Active Directory
---
> *This post was originally posted on Carl Webster's site [here](https://carlwebster.com/bart-jacobss-toolbox-copyadgroupmembers/)*

Another easy, simple addition to my Toolbox: a PowerShell script to copy group members from one AD group to another.

Why? Because I recently needed to do precisely that: after having created a new AD Group, I needed it to have the same members as another AD Group. You can copy AD users, but not groups. Honestly, it was my initial thought I would be able to find this out there somewhere. I didn't. Some scripts I found took a user account as the basis and copied "Member Of" to another user. That's not what I needed. Other scripts were too "basic" like not offering support for an AD Forest with multiple domains.

So I decided to create my own. From the start, I decided I wanted something of a GUI. Nothing fancy, nothing custom. I have used Out-GridView before, and it would do the job perfectly this time around too.

The general idea was to make this publicly available, not just for my single use case. Hence the decision to put some checks in place, without taking it too far and over-complicate things for a simple copy script.

For example, the script checks if you selected the same AD group as source and destination. At the same time, I didn't take AD Group Scopes into account and their specific membership constraints, etc. A simple Try-Catch to capture errors is just what I need for now.

Finally, Github is all the rage right now, so I thought I would give it a go.
You can find the Repo [here](https://github.com/Cloudsparkle/CopyADGroupMembers).

I'll try to get this uploaded to the PowerShell Gallery as well.
> *Update: I have successfully published the script [here](https://www.powershellgallery.com/packages/CopyADGroupMembers/1.0).*
