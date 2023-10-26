---
layout: post
title: "Toolbox #0020: CTX-FixSSLCertOnDDC"
tag: [Powershell, Toolbox]
published: true
---
Synopsis: let's fix and future proof the use of SSL on a Delivery Controller

Today's topic is some basic security. As a Citrix admin, that means you would probably have used (or looked at) KB articles like this one: https://support.citrix.com/article/CTX218986/secure-xml-traffic-between-storefront-and-delivery-controller-7x.

It's old but still relevant. But it's not exactly clean and easy to follow. Speaking about the following, if you follow the KB to the letter, there is a scenario where you could run into trouble. More specifically, I am referring to binding a certificate on the Delivery Controller.

Do you want to know how I know that? Well, it happened to me not that long ago. The article discusses using "netsh" to bind the certificate to the IP address of the Delivery Controller. The problem with that approach is that if you need to change the IP of your delivery controller, everything stops working. In my opinion, a better way is to bind the certificate to 0.0.0.0. That will always work, no matter what IP you decide to configure. It would certainly have saved me some pain.

There are also several guides out there that try to make the process easier. At least those guides provide some much-needed structure. But there is no script out there that solves this challenge. That's because there is simply no PowerShell equivalent for netsh.

But you can still use netsh in PowerShell and try to make sense of the output. And that's what I did. The script will first verify if it's running on a Delivery Controller and only proceed if that's the case. It will also gather all installed certificates (so you need to install at least one yourself). If there's only one, the script will use that. The script will present you with a certificate choice if there are more.

Then comes the tricky part, or where the magic happens. The script will remove all bindings. And create a new one on 0.0.0.0:443 using the selected certificate. For these last two steps, the script uses netsh.

All we need to do now is to set the new configuration active. To that goal, the script restarts the Citrix Broker Service as a final step.

This one goes without saying: please be careful when running scripts created by others on your systems.

As always, you can find the script on GitHub [here](https://github.com/Cloudsparkle/CTX-FixSSLCertOnDDC).  

Stay safe!
