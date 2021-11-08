---
layout: post
title: "QuickPost #001: AD Password expiration date reset"
tag: [QuickPost, Active Directory]
published: true
---
Synopsis: Two ways to reset AD password expiration date

No extra tool in the toolbox this time, but something small that may come in handy. My very first QuickPost.

There are still a lot of companies out there that insist on regular password changes. But, unfortunately, that change does not always come at a convenient time. A bit like Windows updates, let's say.

In other words, there are times that a reset of the password expiration date is just what you need. There are two easy ways to accomplish that.

#### The first way - pwdLastSet attribute

If you don't know how to get to this attribute, this blog post is intended not for you.

The steps:
1. Set the pwdLastSet attribute to 0. Make sure to hit OK (or confirm)
2. Set the pwdLastSet attribute to -1. Again, hit OK to confirm

At this point, pwdLastSet will change to today's date and time. And your password is good to go again.

#### The second way - Account options

This one is even more straightforward. Go to the account options.
The steps:
1. Check "User must change password at next logon" and hit Apply.
2. Uncheck "User must change password at next logon" and hit Apply.

If you were to check the pwdLastSet attribute, you would see the same thing happened: the date and time of the moment you hit Apply is in there.

Either way, the password expiration date has been pushed back. Hopefully to a more convenient time.

Stay safe.
