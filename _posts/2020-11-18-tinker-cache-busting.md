---
title: How to Restart Tinker
permalink: /tinker-restart
date: 2020-11-18 21:00:00 +1100
tags: [tips, laravel]
description: How to keep Tinker up to date with code changes in Laravel PHP with a simple refresh trick
---

I was stuck with an annoying scenario today:

I was making changes to a utility class I'd written in Laravel to work with the HubSpot API. In order to debug an error I was seeing I needed to make small changes and use Tinker to run the command again.

By design, however, Tinker cannot simply be refreshed or rebooted. You need to exit out of Tinker and start it again. This is a minor inconvenience usually, but when you need to do it dozens of times, it gets pretty tiresome.

Thankfully, this GitHub issue [Tinker must be restarted to take effect](https://github.com/laravel/framework/issues/8504) has a passable solution. You can open Tinker in a loop and have it restart with `CTRL + d`, or close it with `CTRL + c`

```sh
while true; do php artisan tinker; done
```

You can make this easier by creating an alias in your `.bashrc` or equivalent.

I modified this slightly, as I was running Tinker in a Docker container:

```sh
while true; do docker-compose exec app php artisan tinker; done
```

It's a small improvement, but such improvements restore santiy, don't they.

{% include twitter_plug.html %}
