---
layout: post
title: "Toolbox #0013: IISLogMonitor"
tag: [Powershell, Toolbox]
published: false
---
Synopsis: Continuous IIS Log file monitoring

There are times when a Quick Post (in this case Quickpost #0003, [here](https://www.cloudsparkle.be/2022-02-07-Remote_registry_part2/)) becomes used in a full-fledged tool in the Toolbox. Initially, I planned for QuickPost #0002 to become a part of this tool. Plans change.

This toolbox item is even related to one from some time ago. Quite a long time ago already. Please read all about it [here](https://www.cloudsparkle.be/2020-07-10-GetIISLogEndpoints/).

Let's start with a small recap of that last one. It gathers all unique endpoint IPs in IIS logs. After attempting to resolve those IPs, the script exported that data to a CSV.

This tool builds on that idea but adds a "real-time" component. That's just a fancy way of saying that this tool runs all the time. So it's constantly  "monitoring" the IIS log for new IPs that appear. The first step in that process is to find the current IIS log file. So, when you run the script for more than 24 hours, it will automatically pick up the new log file when IIS switches to it. There is also some basic logic in there that makes sure that:

- the log file is only processed if the number of IPs does not match the number found in a previous run
- if an IP is present in that last run, it's not processed again.

Having IPs is excellent, but we also need to make more sense out of them. So computer names and user names, please!

As I said in the introduction of this article, I originally included the code from QuickPost #0002 for this. But it turned out; it was just slow. And WinRM is not the most reliable either. So that's why essentially QuickPost #0003 was born, and I ended up using that code in this tool. It now uses remote registry capabilities to retrieve the computer name and username.

The script will put those usernames and computers in 2 AD groups, but they don't have to be. It's just what I needed for my problem.

As always, I've published this one on GitHub [here](https://github.com/Cloudsparkle/IISLogMonitor).
