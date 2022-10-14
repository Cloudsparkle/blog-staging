---
layout: post
title: "Toolbox #0018: CTX-AppSwitchDG"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: let's switch some apps around.

Let's set the playing field first. We have some mission-critical business applications published and running on Citrix CVAD servers. The business side needs those applications to be available 24/7 (or close enough).

Now, the servers that those applications are running on need reboots from time to time. For updates and memory leakages, ... you pick your poison.

That sounds like a bit of a conflict of interest. But there are options available, but each comes with its challenges.

For example, you can set up a delivery group reboot schedule, but session hosts in maintenance mode will not reboot.

This led me to a new addition to the toolbox and the subject of this post: CTX-AppSwitchDG.
The idea is to have two Delivery groups, each with its Machine catalog, and switch the applications from one Delivery group to the other. That switch must occur weekly, but not more than once a week.

A very crucial detail is the naming of the delivery groups. They should end with "1" or "2". The script switches applications to the correct DG based on the week number. An even week number means applications should run on the delivery group "2". An odd week number has those applications running on the delivery group "1".

Once the applications have been switched, the script monitors last week's servers, logging off idle and disconnected sessions. After some time, those servers will be void of any session and ready for the final task of the script: do a proper Citrix reboot. Meaning: a reboot that MCS needs to work its magic.

As always, you can find the script on GitHub [here](https://github.com/Cloudsparkle/CTX-AppSwitchDG)
Stay safe!
