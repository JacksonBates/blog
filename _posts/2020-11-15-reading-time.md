---
title: How to Add Reading Time to Jekyll
permalink: /reading-time
date: 2020-11-15 23:30:00 +1100
tags: [tips]
---

One of the resonably simple things I've wanted to add for a while is an estimated reading time note on all my blog posts.

I like that you can hack something like this together quickly and add it to Jekyll sites.

Here's how I did it.

## Calculating the wordcount (roughly)

The first thing to do is figure out how many words are in a post. This only needed to be a rough count for my purposes, so I basically grabbed all the text within the element wrapping the post content, split it by word, and then count them.

My posts are all in an article element with the class `post` so this was as easy as `document.querySelector('.post').innerText.split(' ').length`.

I used the rough calculation of 300 words per minute, and just round up or down to the nearest minute.

The final snippet, saved as the include `readingtime.html`, looks like this:

```html
<script>
  document.addEventListener("DOMContentLoaded", (event) => {
    var wordcount = document.querySelector(".post").innerText.split(" ").length;
    var minutes = Math.round(wordcount / 300);
    var unit = " minutes.";
    if (minutes === 1) {
      unit = " minute.";
    }
    document.getElementById("readingTime").innerText =
      "Reading Time: " + minutes + unit;
  });
</script>

<div id="readingTime"></div>
```

Then all I needed to do was add the `include readingtime.html` to an appropriate spot on my `post.html` layout.

And that was it - minimal fuss, autocalculated reading time estimates on all posts historical and going forward.

{% include twitter_plug.html %}
