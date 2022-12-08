---
layout: post
title: "Toolbox #0019: CTX-FixHostingConnection"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: let's that Vmware hosting connection.

Every Citrix admin comes across this screen at some point in their career:

![VCAError](/img/VCAError.png)

Something happened to the certificate used in communication with vCenter. Of course, that can be a lot of things, but whatever the case, it's a pain in every case.

Some Citrix KB articles try to cover this: https://support.citrix.com/article/CTX138640/errorcannot-connect-to-the-vcenter-server-due-to-a-certificate-error and this: https://support.citrix.com/article/CTX224551/delivery-controller-cannot-contact-vcenter-server-after-certificate-update-on-vcenter, but they make it way too complicated for my liking. So when I needed to solve this issue the other day, I came up with a plan:

1. Create a new hosting connection. That will install the new vCenter certificate on all Deliver Controllers and database if you choose to select the option "Trust this certificate."
2. Get the SSL thumbprint of that new connection.
3. Replace the SSL thumbprint of the broken connection with the one from the new connection.
4. Clean up the new hosting connection.

If I had the desire to perform these actions manually, I would not be writing this post. So I created a little script designed to run on a Delivery Controller, that takes care of those steps for the most part. You will still have to create the new hosting connection yourself. 
I did include the cleanup function, so let this be a loud and very clear warning: use this script at your own risk. I'm not taking any responsibility for any issue! And I'm asking if you are sure, you know, to be sure.

I could have stopped there, but I wanted to include something extra.   What kind of extra do you ask? The script will ask you to provide credentials for your service account. So I assumed that there would be a lot of environments that use Active Directory for those. And I wrote some code that verifies the credentials you entered. If they are invalid, the script will keep asking you until you enter working credentials or press cancel.

As always, you can find the script on GitHub [here](https://github.com/Cloudsparkle/CTX-FixHostingConnection).  

Stay safe!
