---
layout: post
title: "Toolbox #004: GetIISLogEndpoints"
tag: [PowerShell, Toolbox]
published: true
---
Synopsis: A PowerShell script retrieve all unique endpoints out of IIS Logs

Let's start by kicking in an open door: IIS Logfiles are not the most administrator-friendly logfiles out there.
That being said, they often obtain some very useful information.

Like, you want to know which endpoints are still configured for your old Citrix Web Interface or Storefront server.
Or, who's still accessing the old SharePoint server nobody really cares about (you think).

Sure, there's Splunk, Datadog, PowerBI, Microsoft LogParser (Studio), but they all share the same "problem": it's not an easy quick fix for your problem.
You just want to have a list of endpoints that have been accessing a webserver. That's it.

Not that long ago, I was facing that exact problem. So I wrote up some PowerShell.
I like to keep things simple, so the script isn't all that complicated.

It will process all logfiles (*.log) in a certain folder, like C:\logs for example. Including those in subfolders.
Next, it will import all that data into an temporary CSV. Why? It just works easier (and faster?)
All unique IP addresses will be fetched, and try to get a hostname resolved using the DNS server of your choosing.

In the end, it will dump everything in an easy to use CSV file, located in your %TEMP% folder.

As always, you can find this script on my GitHub Repo [here](https://github.com/Cloudsparkle/GetIISLogEndpoints).
