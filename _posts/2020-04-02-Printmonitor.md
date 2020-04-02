---
layout: post
title: "Toolbox #002: PrinterMonitor"
tag: [Powershell,Toolbox]
---
Synopsis: a PowerShell script to monitor shared printers on a print server.

Some of you may have seen my scripts for monitoring good old XenApp 6.5 servers I published on Carl Webster's site. For reference: you can find them [here](https://carlwebster.com/bart-jacobs-toolbox-monitoring-part-1/) and [here](https://carlwebster.com/bart-jacobss-toolbox-monitoring-part-2/).

Those scripts provided me with the basic framework for other scripts. In this post, I'll be discussing the first one, so stay tuned for more!

As with all my scripts, I try to solve a real-world problem. In this case, monitor printers on print servers. Printers are not cool, not sexy, but when they don't work as users expect, all hell will break loose. I'm sure we've all been there at some point.

So, what does this script do? First of all, it will read the print servers out of a simple text file. The script checks for the file's existence and makes sure it is not an empty file.

For each print server in the file, the script will check if the hostname is pingable. If not, the script will skip this hostname. We all make typo's in text files, don't we?

For every successful pingable server, the script will then start with the real work. It will gather all shared printers, check their queue state, and identify the IP address of the printer port used. That port will be tested for ping connectivity as well. I'm using the Ping function again, and not the PowerShell Test-Connectivity commandlet. Why? The Ping function is much faster, and I don't like waiting for timeouts.

When all tests and checks have finished, the script will put all results in an HTML file. That HTML file can be mailed, shared, … that's up to you.
One more thing, the script is designed to loop continuously. There's a "sleep" parameter in case you want to run the script staggered, resulting in a more frequently updated HTML file.
I've made this script also available on GitHub, and you can find the repository [here](https://github.com/Cloudsparkle/PrinterMonitor).
