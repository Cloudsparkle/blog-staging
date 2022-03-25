---
layout: post
title: "Toolbox #0014: FAS-CertCheck"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: Check certificates for Citrix FAS.

When something goes wrong with Citrix FAS, certificates are the prime suspects. The Authorization certificate is the key player here.

By default, those certificates will last for two years. The bad thing is, there is no actual clear warning when that expiration date is approaching, or worse, has passed. So the one thing you will see is users complaining they can no longer launch published applications.

In more recent versions of FAS, the certificate is there in the FAS GUI. But still, that's not something you open every day. So, where are those certs stored? Unfortunately, I could not find a clear answer in the documentation. I found out they are stored in the Personal certificate store of the "Network Service" account. You can not log on interactively with that account. You can't even open mmc.exe, add the Certificates snap-in and choose to open it for a service account. The one thing that does work:

```
PsExec64.exe -i -u "nt authority\network service" mmc
```

PsExec is part of the Sysinternals suite. So the next step is to load the Certificates snap-in, and you can see the certificates and, more importantly, the expiry dates.


And now to the fun part. You don't have to run mmc.exe; you can also run PowerShell. And run the CertCheck.ps1 from my toolbox. The ultimate goal of that script was to write an alert to the event log. However, that's not possible. The CertCheck.ps1 needs to run as the "Network Service" account. And that account does not have the right to write to the event log. So instead, the CertCheck script will output a CSV file, which can be picked up by another script (WriteEventlog.ps1).  

The script loops through all certificates, finds the Authorization certificate, and determines if there is a need for action. It will generate a message if the certificate has already expired or expires in 1/7/30 days. This should give you ample time to take action. 

You should be able to run the CertCheck.ps1 script as a scheduled task using the "Network Security" account. And a separate scheduled task for the WriteEventlog script.

You can find both scripts on my GitHub [here](https://github.com/Cloudsparkle/FAS-CertCheck).

Stay safe!
