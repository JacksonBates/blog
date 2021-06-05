---
title: "Hacking an Optus Sagemcom F@ST3864V2 router to change DNS settings"
permalink: /optus-router-hack-dns
date: 2021-06-05 22:30 +1100
tags: [hacking]
description: How to change DNS settings on a locked down Sagemcom F@ST3864V2 router provided by Optus
---

I've recently installed a Pi-Hole on my home network. In order to set this up you need to change the DNS settings for your router to try to route everything through the Pi-Hole.

On most routers, this is not a hard setting to change - but I'm using a router provided by Optus from many years ago, and they have it arbitrarily locked down to stop people messing with it.

Specifically, the router in question for me is the Sagemcom F@ST3864V2.

I'm publishing the following information on the understanding that if you attempt to do anything I explain, you are an adult and accept that should you brick your router, you'll need to go buy a new one.

Do not attempt this on hardware you do not own and cannot afford to replace.

But assuming you are a grown-up: here's what I did.

## Goal

What we are trying to do is access the advanced setup options that can only be accessed by the Admin user.

## Cracking admin and changing DNS

Optus does not want you to do this. They'll tell you this is not possible. That means if you break it, they will likely not be too sympathetic.

The admin user is hidden - it's not obvious that it exists from the user drop down you see in various places.

Luckily, the router has a conf file that contains the admin user information and a lazily obfuscated password!

1. Visit [http://192.168.0.1/dumpcfgdynamic.conf](http://192.168.0.1/dumpcfgdynamic.conf) to prompt the download of the conf file.

   Note, 192.168.0.1 is my router admin address - yours may vary slightly, but if you've come this far you likely already know yours.

2. Once downloaded, change the file extension to `.html` instead of conf and open it up in your favourite browser (Firefox for me).

3. Look for the line containing admin password, yours will likely be different: `<AdminPassword>WW1Ob1dXbzBhMmM9AA==</AdminPassword>`

4. Copy the password string and convert it from base64

   Bash can do this: `echo WW1Ob1dXbzBhMmM9AA== | base64 -d`

   (ignore trailing % if using zsh or fish shell)

   So that `WW1Ob1dXbzBhMmM9AA==` becomes: `YmNoWWo0a2c=`

5. Then visit: http://admin:YmNoWWo0a2c@192.168.0.1/main.html
   (note lack of = in url string)

6. If prompted for login, user: `admin`, password: `YmNoWWo0a2c=`
   (note = this time)

7. From here you can now access the DNS settings from the Advanced Setup menu.

   As a bonus easter egg, Optus pops up an alert: `Optus does not recommend changing these settings unless you are a proficient computer user.`

8. Write down anything you change, and probably test reverting it just in case something goes wrong, or you decide to change it back 2 years from now and can't remember what you did.

9. The original DNS servers suggested by Optus when I made this change were 198.142.152.164 and 198.142.152.165 (which I'm writing down here JUST IN CASE I ever need them!).

{% include twitter_plug.html %}
