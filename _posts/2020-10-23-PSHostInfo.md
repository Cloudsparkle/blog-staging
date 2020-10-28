---
layout: post
title: "Toolbox #007: PSHostInfo"
tag: [PowerShell, Toolbox]
published: true
---
Synopsis: A PowerShell version of HostInfo.

In December 2016, almost four years ago, I published an article on the excellent site of the equally exceptional Carl Webster. It was another small tool created to fill a need I'de come across. For a trip down memory lane: https://carlwebster.com/another-small-tool-from-bart-jacobs-toolbox/.  

Sure, the download count pales in comparison to the number Carl Webster is producing. Nevertheless, I would never have thought that 600+ people would download my tool.

In 2020, the time has come to revisit this tool. I wrote the original using AutoIT. It was the easy choice back in those days. It was also the only time I ever used that tool. Today, PowerShell is king. At least in my world.

As a reminder: the simple use case for this tool. Its function is to display an icon in the notification area (you know, next to the clock) and when the user hovers over that icon, show the computer name. This can come in handy in all kinds of helpdesk scenarios. Any time the helpdesk asks you to supply the name of the computer (or Citrix/VMWare/... desktop), this is where this tool comes in. It's always available in the same location; the instructions are always the same.  It's just easy and straightforward.

So I set out to rewrite the tool in PowerShell. In all openness, I didn't start with a blank sheet of paper. I did some research first. My script was mainly inspired by:
Denniver Reining - https://bytecookie.wordpress.com/2011/12/28/gui-creation-with-powershell-part-2-the-notify-icon-or-how-to-make-your-own-hdd-health-monitor/.  
Key takeaway: when creating a GUI, don't use a loop, don't use start-sleep, use a Timer Object instead. It's important.

From the start, I knew the result I was aiming for was a finished product: my tool, compiled to an executable, installed by "setup.exe" or MSI.
Getting to that particular endstate quickly introduced its own set of challenges. For example, getting the current running directory sounds simple right? It does sound simple, and then you find out ISE reacts differently to the console, and that behavior changes again after generating an EXE-file based on the PowerShell code. I wasn't the only one dealing with this issue, and this is by far the most straightforward solution I could find:

Kae Travis - https://www.alkanesolutions.co.uk/2019/10/10/obtaining-the-current-working-directory-using-powershell/  
Dave Wyatt - https://powershell.org/forums/topic/compile-ps1-to-exe/

And that's not all. I also decided to use a function to read a config.ini file. My source of inspiration:  
Oliver Lipkau - https://gallery.technet.microsoft.com/scriptcenter/ea40c1ef-c856-434b-b8fb-ebd7a76e8d91

So, what else of my own creative code did I put into the script?

Several things jump out:
1. There's a context menu, customizable through the INI-file; see below.  These customizable options include:
    * Exit
    * Support email
    * Support portal
2. There is also a non-customizable option, "Copy to ClipBoard" that copies the data shown to the clipboard for further use.  

3. The INI-file: settings in that file defines several options: ShowExit, ShowUser, ShowSupportMail, and ShowSupportPortal.
    * ShowExit: shows the Exit command in the context menu, default: 0 (disabled, not showing)
    * ShowUser: shows the logged-on user next to computer name and IP address, default: 1 (showing)
    * ShowSupportMail: shows the right-click menu to create a new mail to support. The email address to send this to is also defined in the INI-file, under SupportMail.
    * ShowSupportPoral: shows the right-click menu to open the Support Web Portal using the default browser. The URL is also defined in the INI-file, under SupportPortal.  

4. The IP address.  That is something the original version didn't have. I didn't use get-netipaddress for retrieving the IP information. Instead, I resorted to a single, one-time ping. That method gives me exactly what I want: the primary IP address. And ping just works everywhere, get-netipaddress does not.  

5. It is showing the computer name and IP in the balloon on two lines. That had me struggle for a while. It works, but you can't align everything properly. So visually, it's a mess. Technically, it works.  

As I mentioned before, it was all about a finished product this time. The first step was easy. I used PS2EXE to convert the PowerShell file into an executable. I've used this tool before, and it's just amazing how simple and effective it works.  

Now that I've got my fancy EXE-file, the next step is distribution. After considering my options, I opted for Inno Setup Compiler through Inno Script Studio. Why? It works, it's simple, and it's easy to get started with. The installer copies the files (EXE, INI, and icon) to a folder and registers the EXE in the Registry for automatic startup. It's a SETUP.EXE, but with silent parameters (courtesy of Inno Setup, that stuff is there out of the box).  

Time to wrap this up. What set out to be a "quick" PowerShell conversion of an existing tool turned into something a lot bigger. "Feature Creep" is a real thing.  I felt it. If that much so, I'm considering doing a "Lite" version, with no options at all. If I decide to publish, you'll read all about it on this blog.

As always, you can find these scripts on my GitHub Repo [here](https://github.com/Cloudsparkle/PSHostInfo).
There is also a genuine release on Github, including setup.exe. Go download this [here](https://github.com/Cloudsparkle/PSHostInfo/releases/tag/v1.0).
