---
layout: post
title: "Toolbox #0016: PS-ScheduleTask"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: Scheduled Tasks done in a special way.

I have never really liked working with scheduled tasks. Somehow, they come across as unreliable.

Most of the time, this shows itself after a reboot. Even though the trigger is set to "At system startup", it fails to execute a lot of the time. Mostly this is because some dependency is still starting. You can configure a delay, but you don't want that a long delay at the same time. The only way of figuring this out is by trial and error.

I found a nice little trick to get this sorted the other day. Instead of using a trigger "At system startup", you can:
- configure the trigger to run "one time" at a specific time
- configure the trigger to repeat the task every minute, indefinitely
- configure the setting "if the task is already running " to "do not start a new instance."

This post could have ended right here, and then it would have become a QuickPost. However, I could not just let this go. So I created a little PowerShell script that creates a scheduled task with the trick mentioned above.

The script also sets up the scheduled task to run as another user, and it will prompt you for the password. It also features a way to customize the timing. There is a variable called $taskminutes. That will do two things:
- the "one-time" trigger will be set for the current time + $taskminutes
- the "repeat every" will also be set to $taskminutes

You can always find the script on my GitHub repo [here](https://github.com/Cloudsparkle/PS-ScheduleTask).


Stay safe!
