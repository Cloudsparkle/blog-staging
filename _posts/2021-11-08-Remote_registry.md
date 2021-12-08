---
layout: post
title: "QuickPost #002: A different way of getting the computer name "
tag: [QuickPost, PowerShell]
published: true
---
Synopsis: Forget DNS, let's use the remote registry to get the name of the computer

Another Quickpost this time. Just too little code to warrant a full-blown tool in the toolbox. For now, anyway.

So let's cut right down to the chase.

I found myself in a position all I had was an IP address of a remote computer. Even it's an AD joined device, DNS would not return the name of this computer.

First of all, I tried to use PowerShell remoting. But, unfortunately, using just an IP address is not as straightforward as I hoped it would be. WinRM just does not seem to like using only an IP address.

Not all was lost because while WinRM seemed to be a dead-end, I was able to use Regedit and connect to the remote registry. So again, this was something I could use.
So, these lines will give me the computer name. And let's just get the name of the currently logged-on user for good measure.

{% highlight powershell %}
$computer = "192.168.1.15"
$RegLM = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey('LocalMachine', $computer)
$RegKeyLM = $RegLM.OpenSubKey("SYSTEM\\CurrentControlSet\\Control\\ComputerName\\ActiveComputerName")
$Computername = $RegKeyLM.GetValue("ComputerName")

$user = (Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName $computerName).UserName

Write-Host $Computername, $user
{% endhighlight %}.

Yes, for the user name, I do use WinRM. Because I can, and I have the computer name at that point.

Stay tuned for more, because this Quickpost will soon feature in another tool in the toolbox.








Stay safe.
