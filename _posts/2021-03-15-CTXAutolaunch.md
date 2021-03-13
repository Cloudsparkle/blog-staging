---
layout: post
title: "Toolbox #008: CTXAutolaunch"
tag: [PowerShell, Toolbox]
published: false
---
Synopsis: A PowerShell tool to launch Citrix Published resources (automatically).

Recently I found myself in need of yet another tool: I needed to autologin into a Windows device (Win10 IoT Thin-client anyone?) and auto-launch a particular Citrix published resource. The autologin to Windows part was the easy one; that's nothing more than a quick registry fix and be done with it.

Now, for the auto-launch of the Citrix published application. There is a KB article out there that pretty much lays it all out: https://support.citrix.com/article/CTX228550.

Seems straightforward enough, right?
Sure...on a single device, with a single user. But what about an automated deployment? It turns out; the StoreID can be different, depending on how much control there is and how things are configured. And just because users like to do things differently. Different Store ID's basically mean: the shortcut person A creates on his machine does nothing for Person B on another device. That's something we need to fix.

The nice part: it's all there in the registry. You need to set up favorites or block favorites altogether; then, everything is a favorite for the registry anyway. Just be careful; workspace uses a different name for a particular registry key. In the end, that's just a little something to cover in a script.

Now, onto the tricky part. After logon, Receiver/Workspace will load. When? That's an excellent question. "It depends". When it does, it takes some time for SSO to sign in. Luckily, there a way around that too. It's all in the script.

With all that "waiting" and loading, you need to give the user something to look at in the meantime. So I decided it's about time to introduce a splash-screen. It uses WPF and has given me some frustrations, to say the least. My source of inspiration was right here: https://www.dev4sys.com/2016/06/powershellwpf-part-iii-how-to-load.html

I kept the very basics only. I stripped a lot out. Because I just needed the splash screen part, the script itself does not require any GUI stuff.

That was the most challenging part of the script. It was getting the splash screen to work consistently. In the end, it all worked out. On one condition: there is a single line of code to make it all just right: "sleep 5".

Yes, that's right. It just needs a little power nap, and then it's good to go. About that, I've compiled, created a setup for it, in the same way I did for PSHostInfo. Get all the technical details right here.

You do need to feed it the name of the published resource, and if it's in the favorites, it will just launch right on queue.

As always, I've published this one on GitHub here. There's a release, too, with a proper setup to get you going.

As always, you can find these scripts on my GitHub Repo [here](https://github.com/Cloudsparkle/CTXAutoLaunch).
There is also a genuine release on Github, including setup.exe. Go download this [here](https://github.com/Cloudsparkle/PSHostInfo/releases/tag/v1.0).
