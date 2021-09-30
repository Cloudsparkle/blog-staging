---
layout: post
title: "Toolbox #011: a simple provisioning tool"
tag: [Powershell, Toolbox]
published: false
---
Synopsis: Provide a simple tool to provision application resources

There is a best practice that goes back to before Active Directory even existed. And it still holds up in today's cloud era.

> If one wants to give access to resources, one uses groups.

This goes for a lot of things. One of them: Citrix published resources.
While I created this Toolbox script for a Citrix environment, anyone can just as quickly use it in other EUC environments.

It's a pretty simple script. The very core of it: it adds and removes users from AD groups.
It all starts with an INI file where you specify which OUs to use. The script will present any AD group in those OUs, so make sure you dedicate those OUs. Of course, you would want to do that anyway because you will eventually need to set up some delegation for your non-admin users.

I've added an OU for Citrix published resources and one for Qlikview application roles in this version of the script. This is because those are the ones I needed in this particular project. Changing and expanding these options is a reasonably straightforward process.

From there on, I just use an Out-Gridview to create a simple menu structure:
- add user
- remove user
- list user

I don't know about your AD naming policy; chances are the name of an AD group gives you a clue what's it about. However, to make sure, the script is only displaying the Description field. My recommendation: put something meaningful in there, like the Display name of the Citrix Published resource.

As always, I've published the script on GitHub [here](https://github.com/Cloudsparkle/PS-ADUserRoleProv).
