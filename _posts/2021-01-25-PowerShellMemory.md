---
layout: post
title: "Running PowerShell 24/7 and memory usage"
tag: [Powershell,Blog]
published: true
---
Synopsis: Handling memory usage in 24/7 PowerShell scripts

In any kind of migration scenario, PowerShell is simply a must-have tool. It doesn't matter what you are migrating; the versatility of PowerShell will always have your back.

And yes, so I found myself migrating some users of a legacy EUC platform to a more recent iteration. A multitude of applications resulted in an equal number of PowerShell scripts. In terms of logic, those scripts are reasonably simple, to be honest. It always comes down to moving users around in AD and getting some files in the right places as well. I'll go into some more detail in a future blog post. Because... it's never as straightforward as one might think upfront.  

One thing those scripts do have in common: they need to run continuously, as in 24/7.  Yep, indeed those "while ($true)" loops.

Before we get to the very point of this post, let's get this out of the way. I'm aware a lot of people will say:
- Powershell is not meant to do that.
- Powershell is not designed to run all the time.
- Powershell lacks the memory management of C# and other programming languages.  

These may very well be accurate statements. But PowerShell is my weapon of choice and the one I have become quite comfortable with.

So, there I was running a couple of those scripts. Until I realized they were getting slower with each loop. Then I looked at Task Manager and immediately saw the root issue of that slowness: memory usage was through the roof. Sure, I could restart those scripts by hand every day or so. But that defeated the very purpose of those scripts: automation.
So I went on the hunt. The solution I found everywhere:  
> "[System.gc]::Collect()"  

This command triggers .NET memory garbage collection to be run. And memory usage reduced as a result.
So after adding this to my infinite loop, I saw Powershell memory usage actually drop after each loop. What a beautiful sight. Please make sure the garbage collection can actually do it's thing, so a little "sleep" can be handy.  

Just make sure to run the script in a PowerShell session and not in ISE. I know it can be tempting to do some quick tweaks and start the script loop again. Please don't do it. Memory usage will be through the roof, no matter what you do to optimize.  

You can actually get real nerdy and track memory usage and garbage collection results by running these commands.
Before:
> write-host "Memory used before collection: "([System.GC]::GetTotalMemory($false))"  

After:
> write-host "Memory used after full collection: $([System.GC]::GetTotalMemory($true))"  

Bottom line: for anyone running PowerShell scripts in an infinite loop: insert that command to get your memory usage under control. And don't run in ISE.
