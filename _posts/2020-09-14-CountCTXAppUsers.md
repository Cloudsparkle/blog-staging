---
layout: post
title: "Toolbox #005: CountCTXAppUsers"
tag: [PowerShell, Toolbox, EUC, Citrix]
published: true
---
Synopsis: A duo of PowerShell scripts to count the number of users per Published Application.

Another addition to the Toolbox. And be warned: double trouble ahead!

Initially, I set out to write just one script. A script with a very simple purpose: to count enabled AD users for each (enabled) published Citrix application.
Citrix as in CVAD (Citrix Virtual Apps and Desktops), just like users call to tell you: "the Citrix server is acting up again". We've all been there.

But... the reality is that there is not just one version of the "Citrix server" out there. Not yet, anyway. Some day, all XenApp 6.5 servers will have become extinct. But I don't know about you, but that day hasn't arrived just yet in my world. All this just to tell you, there's two versions of the script: one for CVAD 7.x, and one for XenApp 6.5.

So, back to the script "design" if you will. You'll need to configure one single thing in both scripts: specify the ZDC or DDC to be connected to.
Both scripts require the Active Directory module to be present.
Both scripts also need the corresponding Citrix PowerShell plugins.

One could assume that outside of the Citrix PowerShell commands for each platform version; the code is otherwise identical.
Well, you know what they say about assumptions...

At first, the scripts will gather all enabled published applications. Not all of them, only the enabled ones.
They will extract all AD users and groups used for publishing. Yeah, I know, you should only use AD groups. Well, remember what I said before about assumptions? Right...

And this is the most significant difference in the two scripts: how Citrix PowerShell modules return that information... To say it's different is an understatement. Actually, I don't get why this would have changed.
In XenApp 6.5 world, it was easy and straightforward. In the new world, things just got complicated.

Anyway, the script will go through all groups used (yes, it's recursive, didn't I mention that?) and count all enabled user accounts.
When all counting is done, you'll get a nice CSV file with the info you need: application name, groups and/or users used, and the total number of enabled accounts.

As always, you can find these scripts on my GitHub Repo [here](https://github.com/Cloudsparkle/CountCTXAppUsers).
