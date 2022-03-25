---
layout: post
title: "Toolbox #0015: PS-Applaunch"
tag: [Powershell, Toolbox]
published: false
---
Synopsis: Published application launcher

First of all, I admit: I have felt a bit "dirty" ever since fellow CTP James Ranking put this post out into the world.

Why? James feels that logon scripts are "old" and "dirty".
Read all about it [here](https://james-rankin.com/articles/quickpost-how-to-start-a-process-when-a-citrix-published-application-launches/).

Well, there is one thing I can relate to: when looking at a VBS logon script, I did feel old.

Speaking of old, the basis for this tool started in need for a launcher tool to start Navision-based applications. They tend to have several command line parameters, and each of them can be pretty lengthy. In other words: you ran into some limits rather quickly. I'm not going to publish that tool publicly, given the specific use case. If anyone is interested, you know how to get in touch (hint: Twitter works excellent).

Another reason for that launcher tool to exist is the ability to wait for something to be completed before starting the actual application, like a logon script, for example.

Yes, exactly the use case James was referring to. And I took a different approach. Having just changed the configuration of a few hundred published applications, I didn't feel that the need to change that, is a blocking issue. Yes, it's a one-time change, but it can be planned and executed in steps. There's no need for a big bang. Just start with the applications that generate help desk tickets, and it will all be okay in the end.

So, back to technical stuff. I set out to create a framework application, a launcher tool to launch all other applications.

Back in toolbox #0008 ([here](https://www.cloudsparkle.be/2021-03-17-CTXAutolaunch/)), I had some first experience with a splash screen. So I built on that experience and created this App launcher tool.

The features:
- fully customizable splash screen
- possibility to add command-line parameters
- ability to launch another program before the main executable, and if needed, wait for that process to finish first.
- ability to wait for the logon script process to finish before launching the main executable
- possibility to add command-line parameters
- ability to import a REG file before starting the primary executable.

An INI-file is used to store all the configuration options. Let's go over them in an example.

Demo.ini:
```
[LAUNCH]
AppEXEPath = C:\windows\explorer.exe
AppCommandLineArgs = ::{2227A280-3AEA-1069-A2DE-08002B30309D}
AppImportRegFile = 0
AppRegFile =
AppRunFirst = 1
AppRunFirstEXE = c:\windows\notepad.exe
AppRunFirstCommandLineArgs =
[CONFIG]
WaitForAppRunFirstEXE = 1
WaitForLogonScript = 1
WaitForLogonProcess = wscript
TitleLabel = Citrix App Launcher
TitleForeground = Yellow
LoadingLabel = Getting Stuff Ready
LoadingForeground = Black
BackgroundColor = #db0f16
```

Demo.ini explained:
```
[LAUNCH]
AppEXEPath = full path to main executable to be launched
AppCommandLineArgs = any command-line arguments for that main exe
AppImportRegFile = Import a reg file before launching (1 = yes, 0 = no)
AppRegFile = In case AppImportRegFile is 1, import this registry file
AppRunFirst = Run another EXE before the main EXE (1 = yes, 0 = no)
AppRunFirstEXE = In case AppRunFirst is 1, run this EXE before main exe
AppRunFirstCommandLineArgs = Any command-line arguments for the RunFirstEXE
[CONFIG]
WaitForAppRunFirstEXE = 1 = wait for AppRunFirstEXE to finish (1 = yes, 0 = no)
WaitForLogonScript = wait for logonscript process to finish (1 = yes, 0 = no)
WaitForLogonProcess = name of the logon script process
TitleLabel = Title of the splash screen
TitleForeground = Color of the title of the splash screen
LoadingLabel = Text for the loading label
LoadingForeground = Color of the Loading label text and animation
BackgroundColor = Background color of the splash screen
```
As always, I've published this one on GitHub [here](https://github.com/Cloudsparkle/PS-AppLaunch). This one also has an executable and installer. Please be aware I created this EXE with the fabulous PS2EXE. This may result in false positives reported by several AV vendors. Please take care and add these to the exclusion lists before you deploy. You don't want to get the call that some AV is wrongly blocking all your published applications from starting.

Stay safe!
