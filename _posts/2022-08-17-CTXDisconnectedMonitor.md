---
layout: post
title: "Toolbox #0017: CTXDisconnectedMonitor"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: Taking care of disconnected sessions

Every tool in the toolbox exists for a reason. I ran into a problem, and I wanted to solve it. Pure and simple. This one is no exception.

Disconnected sessions can be a blessing and a worry. In this case, the concern was that I could not have any disconnected sessions for a specific application. The application just would not behave when reconnected.

And yes, you can set a Citrix policy to log off disconnected sessions after a specific number of minutes. But this policy was of no use to me. For example, the policy can target users or delivery groups, but those do not fit my use case. And even with the lowest possible number of minutes, it would still be too much.

Hence, I created a new tool. The script is meant to be running on a batch server. Therefore, it is designed to be able to reach out to multiple environments and keep them all in check. An INI file stores the configuration details for those multiple environments and applications to monitor.

This is the structure of the INI file:
```
[DDC1]  
PublishedApp1 = Application number 1  
[DDC2]  
PublishedApp1 = Application number 2  
```
The script uses sections for the names of the Delivery controllers. The keys below each section are the applications to monitor for disconnected sessions.

When the script finds a disconnected session, the session is logged off.

Hold on; a session is not always just one application, right? There could be other applications running in that same disconnected session. Therefore, the script can not just look at the application that launched the session in the first place. Instead, it needs to look at all the published applications in the session, and if it finds a specified application, the script takes action: logging of the session with all applications inside it.

I did consider putting some logging into the script but decided against it. Why? Every action the script takes is already visible in standard logging in Citrix Studio.

As you have learned from a post a while back (here), I also included some memory cleanup to be done. This script does need to keep on running.

As always, you can find everything on my GitHub [here](https://github.com/Cloudsparkle/CTXDisconnectedMonitor).

Stay safe!
