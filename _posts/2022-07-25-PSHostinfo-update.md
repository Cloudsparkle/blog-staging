---
layout: post
title: "QuickPost #0007: PSHostInfo updated"
tag: [QuickPost, Powershell]
published: true
---
Synopsis: PSHostInfo, updated

Remember PSHostinfo? I won't blame you if you don't, but feel free to have a look at it [here](https://www.cloudsparkle.be/2020-10-31-PSHostInfo/).
It's time for an update. It's not a big update; it does not deserve a full-blown blog post. A QuickPost will do just fine.

What has changed?
I updated the code to include minor fixes in reading the INI file values (or lack thereof). Let's call those minor bug fixes and performance improvements.
Next, two new actions:
- Citrix workspace app, icon refresh
- Citrix workspace app, reset user config  

Both actions will only be available if the option is turned on in config.ini and Citrix Workspace App is present on the system.

I updated my GitHub repo [here](https://github.com/Cloudsparkle/PSHostInfo), including an updated installer of the compiled executable. Caution: I used PS2EXE for this one so that it might trigger some false positives in your AV.

Stay safe!
