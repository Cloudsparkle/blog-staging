---
layout: post
title: "QuickPost #003: A different way of getting the computer name - Revisited"
tag: [QuickPost, PowerShell]
published: true
---
Synopsis: Forget DNS, let's use the remote registry to get the name of the computer and the user

Remember the last QuickPost? This one is loosely based on that one. However, it just takes things a step further.

#### What stayed the same?

The script uses the remote registry to "resolve" the computer name when given an IP address.

#### What changed?

The "old" code still relied on WinRM to get the logged-on user name. It seemed fine at the time, but WinRM can be tedious and just slow.

So, in this code below, I'm also using Remote Registry to identify the user account currently logged on. It wasn't as straightforward as I assumed it would be at first. But, once I identified the registry key I had been looking for, the rest was easy.

```powershell
$computer = "192.168.1.15"
$RegLM = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey('LocalMachine', $computer)
$RegKeyLM= $RegLM.OpenSubKey("SYSTEM\\CurrentControlSet\\Control\\ComputerName\\ActiveComputerName")
$Computername = $RegKeyLM.GetValue("ComputerName")

$RegKeyLM2 = RegLM.OpenSubKey("SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Authentication\\LogonUI")
$User = $RegKeyLM2.GetValue("LastLoggedOnUser")

$aduser = $user.Split("\")
$aduser = $aduser[1]                

Write-Host $Computername, $aduser
```

In the previous "version" of this QuickPost, I kind of made the promise this code would feature in a new tool in the Toolbox. That was the original plan, but as you will (hopefully) read, later on, plans change. So I can tell you that this is the actual code that got integrated into the tool. Why? It's just much, much faster. That's all.

Stay safe!
