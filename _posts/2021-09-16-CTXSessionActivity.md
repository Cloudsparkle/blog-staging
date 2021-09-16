---
layout: post
title: "Toolbox #009: Citrix UPM fix"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: Count those session logon and logoff events

Inspired by a question of fellow CTP Joe Shonk, a new addition to the toolbox is born.

It's even a twin!

Before we get into that, let's take a step back and look at the problem at hand. Today, there does not seem to be an easy way to produce numbers on how many Citrix CVAD session logon and logoff events happen over a period of time. In certain situations, this can be a very valuable metric to have.

Enter Powershell. What else did you expect?
And the twins, because I created two scripts: one to count logons, one to count logoffs. Why? Let me explain the basic logic of the scripts first. I'm sure you'll get the answer down the line.

The script continually loops through all sessions and creates an array of session keys it encounters. It does not look for all sessions, but it looks specifically for two states a session can be in: LogonInProgress and LogoffInProgress. Because looking for those two states in a single loop/script could require logic that just may take too much time and cause the script to miss events. And while we are on the subject, let me add this disclaimer right here: I'm not providing any guarantee those scripts will catch all logon/logoff activities.

We do need a way to break the loop because, at a given point, we want to stop counting. So I opted for the press of a button, and I took code I found here: https://stackoverflow.com/questions/150161/waiting-for-user-input-with-a-timeout. I tweaked it a bit to my needs, but it's a framework to break out of a loop using a specific key press.
Now that we are out of the loop, we have an array of session keys that had the specific logon or logoff state. Because it can take some time to perform either of those things, the script will likely have the same session key more than once. So the final step is to make sure we only have unique session keys and count them. That's it. The script finishes with the number of logon/logoff activities it has seen and the total runtime.

As always, I've published these scripts on GitHub [here](https://github.com/Cloudsparkle/CTXSessionActivityCounter).
