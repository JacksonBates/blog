---
title: setState wasn't working - annoying bug postmortem!
permalink: /setState-fail
date: 2019-05-07 11:33:00 +0800
tags: [react, post-mortem]
---

I encountered a very annoying bug in a piece of basic React code yesterday, and it took me and another experienced developer far too long to spot the problem.

Here is the screenshot I posted to Slack after spending no small amount of time already trying to figure it out:

![setStateFail]({{ site.baseurl }}/assets/img/setState-fail.png "setState bug screenshot")

We have an annoying issue in our product where an informative screen element truncates long messages, so we wanted a simple solution of rendering a modal with the full message when the truncated version was clicked. VERY EASY to do with React, right?

So the code above purports to do that. Click on the truncated message element: modal pops up; click on the 'Ok' button on the modal: modal is dismissed.

Here is simple reproduction of the bug on CodePen:

<p class="codepen" data-height="229" data-theme-id="0" data-default-tab="result" data-user="Malgalin" data-slug-hash="PvwRmv" style="height: 229px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Bug Demo 7-5-19">
  <span>See the Pen <a href="https://codepen.io/Malgalin/pen/PvwRmv/">
  Bug Demo 7-5-19</a> by Jackson Bates (<a href="https://codepen.io/Malgalin">@Malgalin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

The only real modifications I've made to the above app are the conditionally rendered div in place of the modal, and the click counter that proves that the close handler method works and can set the state. You can click the `babel` tab above to see the code, and the `result` tab to toggle the app view away.

## Diagnosing the problem

If you Google any version of 'setState is not working' you will encounter a gazillion StackOverflow answers and blog posts that will tell you that the issue is that `setState` is asynchronous.

Great, who cares? That's not the problem here, right? Because we are calling an identically formatted setState function to dismiss the modal as the one that made it appear.

We added console.logging within the setState callback to ensure that the setState code was being reached. It was. Then we added a click counter like the one in the reproduction to prove that we could update state with that exact method. We could.

Eventually we determined that there must be a race condition somewhere, somehow. Even though we were certain nothing else was trying to set the state, something must have been.

Look again at the code.

- The `<Container>` has the initial onClick listener.
  - Clicking the `<Container>` triggers setState.
- The `<InformationDialog>` has its own onClick listener.
  - Clicking the `<InformationDialog>` triggers setState...
  - but also, something else is triggering setState again with a competing value.

Have you spotted it already?

<p class="codepen" data-height="224" data-theme-id="0" data-default-tab="result" data-user="Malgalin" data-slug-hash="pmvLxR" style="height: 224px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Bug-Fix Demo 7-5-19">
  <span>See the Pen <a href="https://codepen.io/Malgalin/pen/pmvLxR/">
  Bug-Fix Demo 7-5-19</a> by Jackson Bates (<a href="https://codepen.io/Malgalin">@Malgalin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## The problem is that setState is asynchronous

So, setState is asynchronous...AND the modal was nested in a greedy container.

When clicking the modal, you are also clicking the container again, introducing the race condition.

The solution is to separate the onClick listeners appropriately so you are only clicking one thing at a time.

Fun times were had by all. What did we learn?

Not sure.

Be better, I guess.

<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

{% include twitter_plug.html %}
