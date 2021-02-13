---
title: Why and How I Delete My Tweets After 10 Days
permalink: /ephemeral-twitter
date: 2017-07-26 11:33:00 +0800
tags: [twitter]
description: How to build a tweet bot that deletes tweets after a specified number of days.
---

_I thought I was releasing my flighty words into the world with every tweet, but in reality, Twitter was just a bird cage rapidly filling with every inane utterance I flung into it._

## Why do I do it?

It started when a previous Medium post I published with freeCodeCamp got some attention and plenty of likes and shares.

After the initial buzz died down, I noticed that on a weekly basis there was one user that kept sharing a tweet about it — same format each time — and only a handful of other tweets in his timeline. There was some mention in his bio about ‘ephemeral Twitter’ and I realised he was deleting old tweets automatically, and must also have a bot re-posting previous tweets if there was no new content to replace the old.

Why would anyone do this? Well, he wasn’t alone, and once I was introduced to the idea, it kept popping up as a compelling solution to some of the things that make me uneasy about Twitter.

The sometimes irreverent, usually argumentative, and often silly way in which I currently engage on Twitter doesn’t really serve any long-term goals of mine. The idea that all my nonsense sticks around for any of my students, their parents, or other interested parties to delve into was a little troubling.

My primary reason for regularly purging the historical record of my tweets, though, is that I am regularly finessing my beliefs and opinions — sometimes changing my mind about issues completely.

‘280 characters’ does not really do finesse, though.

Those old tweets just sit there reminding me of beliefs I held long ago, and usually feel like I’ve progressed away from. Keeping them around serves no purpose.

I like the idea that Twitter is conversational and current. I feel like Twitter is supposed to be ephemeral, but in reality it is not.

So, I wrote a node bot that deletes all tweets and unlikes any favourites that are more than 10 days old. I scheduled this to run on a free Heroku instance once a day so it automates the process without me having to think about it, or rent a server for this tiny task.

## How do I do it?

The original version of this post had a detailed line-by-line explanation of how to write the bot yourself. These days I feel like that makes for an unecessarily long post, when all you really want to see is the code. To that end, here is the code on Github: [Tweet Delete Bot](https://github.com/jacksonbates/tweet-delete-bot). The README.md contains instructions on setting it up yourself.

## Set it and forget it!

_You’ve gotta dance like there’s nobody watching,_
_Love like you’ll never be hurt,_
_Sing like there’s nobody listening,_
**_And tweet it like you’re gonna delete it_**.

{% include twitter_plug.html %}

...and then delete it, obviously!
