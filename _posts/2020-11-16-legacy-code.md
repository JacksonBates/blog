---
title: How to Orient Yourself in Legacy Codebases
permalink: /legacy-code
date: 2020-11-16 22:30:00 +1100
tags: [legacy, inherited-codebase-diaries]
---

There was a thought-provoking episode of DevsLikeUs on YouTube that I watched today: [Inherit Legacy Code Like a Pro - The Allen Interview](https://www.youtube.com/watch?v=FGYE83KmoQ8&t=2753s).

There was some great discussion of what legacy code is and, amongst other things, how you might tackle a legacy codebase when faced with one. It's worth watching in its entirety, but I thought I'd add my reflections on that here too, since I have some similar feelings about legacy code, and some alternative strategies for getting to grips with it.

## What is Legacy Code?

There are plenty of definitions of legacy code floating around. Many think of it simply as code they didn't write. Another popular definition is any code without tests. Perhaps a more reasonable definition is code written by someone you don't have access to.

I think of it more like an inheritance: code that has been passed on to you. It's now your responsibility to shepherd the project and help it continue to grow. Much like inherited wealth, your job is to steward it well, and make more. Not only does this imbue it with some respect for the successful work completed by those that came before - it also serves to remind us that we too are building a legacy that will be passed on to others down the line.

Of course, 'legacy code' is a term most often used to describe something complex, complicated, and perhaps convoluted. More often than not, the phrase evokes the notion of technical debt. It's not unheard of that legacy code might also strike fear into the hearts of those working with it - there may be corners of the codebase responsible for important buisness logic that noone has been brave enough to touch in years because it is too important to break, and no-one feels they understand it confidently enough to improve.

## Orienting yourself in Legacy Code

As a solo dev that has inherited a codebase, I tend to think about this from the perspective of someone that only has their own wits available to them to solve problems. Usually, when you are first exploring an existing codebase there are other developers that have been working on the same code around that you can ask questions of. In this case, use them as much as you can.

Assuming you have to go it somewhat alone, though, here's how I'd typically try to get a handle on an existing project.

### Start small

Find a particular part of the system that makes sense to you, and try to understand it. For example, you might examine how a user logs in. Start at the UI level and find where the code responsible for the page and login form live in the codebase. Then look at how they send the user credentials: what route are they sent to? How is the data processed and verified? What happens if they pass or fail? How is the user redirect handled? Etc.

Once you have an understanding of how a single user process happens, you can think about it experimentally. What would happen if you made a change at various stages? Make predictions and test them. Once you can successfully predict the effect of changes to the system, you can confidently assume you have a decent understanding of that part.

Then explore other parts, and so on.

### Examine the structure

Looking at the micro level - how each user work flow is suported by the system - is excellent, but time consuming. It also serves you well to take a step back and try to see the macro view of how the project is structured.

Looking at folder structure can reveal a lot about where the various responsibilities in the codebase lie. Attempt to find where the UI is described and how it is rendered. Look for where and how database actions occur. How are routes defined? Are there automated services or routine, scheduled processes the system relies upon?

Having a good mental map of the codebase will help you find the approprite files, modules, classes, or functions required to make changes of repairs more quickly and confidently.

### Uncover its secrets

Projects will often have config files and secrets files, such as `.env`. Reviewing these can help you understand what kinds of APIs and services the project relies on, so a quick glance at these files can show you some of the broader dependencies that might not be immediately obvious by just looking within the core project code.

### Look to the past

Assuming the project has version control, reviewing the git log, the closed issues or PRs, and the database migrations can help piece together the story of how the project became what it is today. Looking through such records in reverse chronological order is a little like peeling back the layers of an onion to reveal what kind of priorites and issues had been driving development prior to your arrival.

With details like these, although the original developers may be long gone, you may be able to find colleagues with memory of how business priorities shifted to explain why certain decisions in the codebase may have been made. Even without access to those that had technical knowledge of what went before, hearing from those that may have historical insights can help you understand what kinds of business constraints may have been shaping the development work.

### Move slowly and surely

It goes without saying: legacy code has been providing value and serving your users since long before you arrived. If changes are required, check them thoroughly in development before rolling out to production. And if you have the freedom to add tests, do so.

---

Legacy code is code that has been paying the bills. That doesn't mean it's necessarily easy to work with, but the one thing you can usually rely on is the fundamental principle that it must be based on logic. Obscure syntax, convoluted structures, and ignored conventions can slow you down, but finding threads and pulling on them to see where they go and learning to ask the right questions can get you eventually feeling somewhat at home in a legacy codebase.

{% include twitter_plug.html %}
