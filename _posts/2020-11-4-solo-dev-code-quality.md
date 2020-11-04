---
title: Ensuring Code Quality as a Solo Dev
permalink: /solo-dev-code-quality
date: 2020-11-4 23:20:00 +1100
tags: [solo-dev]
---

An interesting question from Twitter:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Anyone working as a sole dev in the project? <br><br>Since you can only depend on lints and there won&#39;t be any senior to review the code.<br><br>How do you maintain code quality?</p>&mdash; Prabin Poudel (@coolprobn) <a href="https://twitter.com/coolprobn/status/1323864098770092033?ref_src=twsrc%5Etfw">November 4, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Obviously, I think about this a lot, since I've been the solo developer at Grace Papers for the last 11 months.

The great thing about being a solo dev is the absolute autonomy you get over your codebase - there is no need to compromise on your preference for tabs vs spaces, trailing commas, omitted semi-colons, or anything else devs like to pointlessly lock horns over.

As Prabin notes above - a linter is all you really need to ensure consistency in this regard.

But if we can all just install Prettier and switch on format-on-save, then what do we need code review for? And can we write good code without it?

## The purpose of code review

When we submit a PR for review, our reviewer is likely looking for a whole range of things. They are only human, but let's assume we catch them on their best day. They might comment on:

### Readability / Coherence / Clarity

The easiest thing for your code reviewer to spot is whether what you've written makes sense to an 'outsider'. You've been thinking about and tweaking this code for anything between a couple of hours, to maybe days or even weeks. A fresh perspective on the code can tell you whether this is something another person (or future you) can maintain with minimal cognitive overhead.

### Functionality / Completeness

Your reviewer should also check whether it does what it is supposed to do. They might do this by reviewing test coverage (if you have added tests), or simply running it and trying various edge cases that their fresh perspective brings to it. Hopefully, your code reviewer knows the business problem you are attempting to solve, so they can assess the completeness of the solution.

### Efficiency

More experienced developers (or simply those with a knack for this kind of thing) can find opportunities for efficiencies in your code. On the one hand, they may recognise that your nested loops can be simplified with a nicer O(log n) solution that improves the resource usage of your code. On the other hand, they may spot an opportunity to refactor and modularize your code to cut down on repetition.

### Best Practices / 'Code smells'

Another category of code intervention a reviewer might provide is to point out where best practices have been missed or 'code smells' have been introduced. This might be as simple as pointing out naming conventions for your language or framework, pointing out things like hard-coded values and magic numbers, or classes have become bloated and out of control.

## Can all this be done alone?

A solo developer's capacity to stay on top of all of the above is determined by a number of factors:

- What is their experience / knowledge level?
  - The more our dev knows, the more they have experienced, the more they are likely to be able to self-review according to the above categories.
- How much time do they have to complete each unit of work?
  - Business pressures might make thorough, diligent, and careful code harder to deliver. The requirement to deliver _fast_ often impacts on the ability to deliver _well_.
- How are their energy levels / focus at the moment?
  - Even the most experienced devs can have their off days and miss things that they'd usually spot and remediate themselves.

All of this can be done, with enough time and experience.

But let's assume a dev with less experience - a category I fall into, as it happens.

The **clarity** issue is hard to do alone - your best bet is to return to code you've written periodically and see if it still makes sense to you. You are unlikely to have time to revisit and fix such code down the track, but you will bump up against code you've written from time to time, and as you re-encounter it you may be able to tighten up what you wrote to clarify it.

**Functionality and completeness** is easier. As I alluded to above, good test coverage can help you think about edge cases beforehand. Although you are the solo dev on your team, hopefully there are other people within your organisation that can do some user acceptance testing (UAT) for you. It is hard to QA your own work, for the same reason it is hard to spot your own lack of clarity: you've just written it and you're thinking about the '[happy path](https://en.wikipedia.org/wiki/Happy_path)'. Getting a second perspective, even from a non-dev, will help you find the edge cases you didn't think of.

**Efficiency**, both in terms of speed and code repetition is a matter of experience and knowledge. The best tool you have at your disposal here is time. Take some time before pushing your commits to ask some questions about your own code: Where are the possible inefficiencies - nested loops, frequent database operations, that kind of thing. Think about other ways to achieve the same outcome in more efficient ways - knowledge of data structures and common alogorithms / patterns can help here. The other thing to spend some time on is learning these. Obviously, if you catch yourself copying and pasting code from within the codebase, you likely have an opportunity to refactor there, too.

Learning **best practices** and how to avoid **code smells** doesn't come with short cuts. If you don't have a more senior developer above you to guide you in this regard, you need to seek this knowledge out for yourself. There are some fundamentals you should learn about your languages, frameworks and database design. To find good material about these you can often find books detailing Patterns / Anti-Patterns, and these can provide excellent proxies for the mentor you don't have. Another place to learn patterns from is open source. Github search is a powerful tool for seeing how other projects implement ideas, and well maintained repos can be incredibly instructive to read through.

If your problem, on the other hand, is that you do not have the time of the energy to do a better job...all you can really do is try your best and agitate within your organisation for either a second dev to help out, or more time to make up for the lack of a second dev.

It goes without saying, that as a solo dev it is entirely likely that there are things I have missed in this post, just as I miss things in my own code. If you have another perspective on this issue, I'd love to hear about it!

{% include twitter_plug.html %}
