---
layout: post
title: "Toolbox #0012: Citrix UPM Reset Tool"
tag: [Powershell, Toolbox]
published: false
---
Synopsis: Citrix UPM reset framework


Back in Toolbox 9 [(here)](https://www.cloudsparkle.be/2021-07-27-UPMFix/), I put some code on GitHub to correct file permissions in Citrix UPM profiles.

Even before that, I wrote a post on running PowerShell scripts 24x7 [(here)](https://www.cloudsparkle.be/2021-05-06-PowerShellMemory/).

Together, they form the basis of a framework for Citrix UPM Profile Resets.

Yes, I'm aware that such a feature exists in Citrix Director, but I took things a bit beyond that. For us admins, a reset is just a push of a button. For users, it's another story. They lose "everything", especially the application settings. Those applications they need to do their work and make the company run in the end. The critical applications for users at a former contract position were SAP and Qlikview. I guess they do sound familiar to a lot of people.

The scripts work together and use an INI file as a configuration source. That INI file contains the names of UNC folder paths, AD groups, and  Citrix infrastructure servers. In addition, some scripts take care of  Citrix UPM resets on a  legacy (XenApp 6.5) farm and the current one (CVAD 7). Finally, the scripts will create a backup with the date and time stamp in all cases. That backup is essential because the application reset scripts will restore the user's application settings for SAP and Qlikview from these backups. This restore will happen automatically after the user has launched those applications for the first time after the UPM reset.

Let's break all the scripts down.

#### FrontEnd
- SelectUser: This is the frontend application. I would be converting this one to an EXE and publishing it to service desk engineers, and so on. Using the script, they can select the user and start the process of the Citrix UPM reset on the legacy and/or current environments.


#### Backend
These are the scripts that need to be running all the time, using an account that has enough rights for AD and file shares.
- ResetCurrentProfile -> main script to reset the profile on current Citrix.
- ResetLegacyProfile -> main script to reset the profile on the legacy Citrix XenApp 6.5.
- RestoreLegacySAPSettings -> when LegacyProfileReset is triggered, this script will restore user SAP settings after first login/logoff on legacy Citrix.
- RestoreCurrentQVSettings -> when CurrentProfileReset is triggered, this script will restore user QV settings after first login/logoff on current Citrix.
- RestoreCurrentSAPSettings -> when CurrentProfileReset is triggered, this script will restore user SAP Settings after first logon/logoff on current Citrix

All scripts use AD groups to process the user and move it to a "Done" group when... yes, that's right, the scripts are done.

I built these scripts some time ago, and just recently I made them publicly available on GitHub [here](https://github.com/Cloudsparkle/UserProfileReset).
