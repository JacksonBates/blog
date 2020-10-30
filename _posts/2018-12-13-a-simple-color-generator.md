---
title: A simple color generator
permalink: /color-generator
date: 2018-12-13 11:33:00 +0800
tags: [noodling]
---

I wanted a quick and easy way to generate semi-random, but consistent colours.

I figured since I could get consistent hex values off of a string using an md5 hash, slicing the last 6 characters from a hash would generate such a colour code.

Here's a little pen that demos the idea:

<p data-height="410" data-theme-id="0" data-slug-hash="roOvpN" data-default-tab="result" data-user="Malgalin" data-pen-title="Color test thing" class="codepen">See the Pen <a href="https://codepen.io/Malgalin/pen/roOvpN/">Color test thing</a> by Jackson Bates (<a href="https://codepen.io/Malgalin">@Malgalin</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script src="https://static.codepen.io/assets/embed/ei.js"></script>

{% include twitter_plug.html %}
