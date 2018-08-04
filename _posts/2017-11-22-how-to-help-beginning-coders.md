---
layout: default
title: How to Help Beginning Coders
permalink: /help-beginners
---

_This post was originally published on [Medium](https://medium.com/@JacksonBates/how-to-help-beginning-coders-c8525b26bba8)_


I am one of those teachers that has been working on transitioning out of the classroom in order to pursue a coding career. As I learn to code, and help others in their coding journey on the [Free Code Camp forum](https://forum.freecodecamp.org), I see lots of teaching take place.

Since I know a lot more about teaching than I do about coding, here is a guide to helping beginning coders, drawing upon some of the best practices we currently know about how people learn.

![An image mashing up the old 'This is your brain on drugs campaign. 3 panels. Panel 1: Text: This is your brain. Image: A whole egg. Panel 2: Text: This is code. Image: A frying pan. Panel 3: Text: This is your brain on code. Image: An egg frying in a pan.](https://cdn-images-1.medium.com/max/2000/1*As74O0E4ea9OG3oiA58rDQ.png)

# Learning theory

There are a number of learning theories you could draw from when considering how best to help others, but the one I’ll be relying upon most is **Social-Constructivism**. (An alternate, arguably opposite, theory is **Social Learning Theory**.)

The grandfather of this theory is Lev Vygotsky, who suggested that people learn best when interacting with others. He also suggested that people are limited in what they can learn _right now_ by their **Zone of Proximal Development (ZPD)**. The ZPD sounds like an intimidating concept, but it really just describes the notion that we are best able to learn the things just beyond our current understanding, with the help of others that have already learned those things.

![A staircase](https://cdn-images-1.medium.com/max/2000/0*FHG904rpH-UK_dW5.jpg)

If you imagine a tall staircase, the ZPD encourages you to climb onto the step just ahead of you, not to attempt leaping up five steps in a single bound. That’s how you twist your cognitive ankles.

# Lessons from Social-Constructivism

What really helps people learn is this:

- Collaboration
- Discussion
- Scaffolding
- Modelling

There is also, very rarely, a case for:

- Just giving them the answer / solving a problem for them…

(But more on that later…)

# Context is key

When helping a beginner coder, especially online, it can be difficult to know what their ZPD looks like. For this reason it is important to ascertain the competence and experience level of the person you are helping.

Often, learners don’t know how to frame their question to reveal their current understanding, so it can help if you begin the interaction by asking clarifying questions. This will help you pitch your help at the appropriate level.

It is tempting, and sometimes useful, to simply direct a learner to the appropriate MDN documentation. With beginners, that is often not the best course of action, though.

# Collaboration

The best way to help someone learn is to both work on something meaningfully together. This idea is the basis of all trade apprenticeships and modern internships.

Working side by side, preferably pair programming, helps build a good relationship and trust — essential ingredients in mentor-mentee relationships.

# Discussion

It’s not always possible, or desirable, to collaborate. The really important part of collaboration, aside from partnering on meaningful work, is discussion. Thankfully that can be had at a much lower cost than full-on collaboration.

As mentioned above, asking questions is crucial to help the teacher understand what the learner already knows. But questions also serve the purpose of helping learners make connections and realise things they didn’t know they already knew. Socratic questions can help learners question their assumptions and force them to reevaluate them, which are crucial coding skills.

# Scaffolding

A common teaching technique employed in schools is scaffolding. This process boils down to the teacher providing less and less structure and support as the learner becomes more capable of proceeding unassisted.

You can leverage this technique when helping beginners when you understand their ZPD. It is important to understand whether someone just needs a nudge in the right direction — _Hey, you may want to look up how AJAX works in jQuery_ — or whether they need something a little more substantial — Hey, you can use `$getJSON(‘http://….’, function(data){…})` to do that…have you use a callback function before?

# Modelling

Related to scaffolding, modelling describes the process of providing similar answers or solutions, but with the particulars removed so the learner can apply the principle in a different context.

By way of simple example, a learner might be stuck reversing a string using string concatenation. Rather than telling them how to do that, you might instead show them a similar function, for example, one that iterates over the items in an array and does something to them, or one that replaces each character in a string, one at a time. You can then ask them to explain what it does and how that might apply to their current problem.

# Helping The Deer in Headlights

Sometimes beginners can get so panicked and overwhelmed that they just freeze up. I don’t advocate ‘just giving the answer’ often, but very occasionally I will.

If it is particularly important to you that the person goes on to greater success in the future, and the problem they are currently facing could be enough for them to swear off coding forever, it could be more important to win the battle for them, so the war is not lost altogether. It’s a fine line, though — you do not want to encourage learned helplessness.

It can be frustrating when a learner simply isn’t getting something, but that is not usually the time to just cave in and tell them the answer.

Some people, while initially trying to help, can slip into macho talk like, _‘Well, no body here is gonna hold your hand — suck it up, princess!’_ Obviously, this doesn’t really help people, especially in beginner oriented communities. No-one leaves that scenario with the dawning realisation that they are indeed a princess that needs to just read the fine manual, so the only purpose it serves is to further alienate struggling learners and disenfranchise from the opportunity to learn more.

One of the prevailing philosophies beginners encounter on the Free Code Camp forum, is that no question is too stupid, and it doesn’t matter if the question has been asked before. We aim to have a community completely open to newbies — and let’s face it, when it comes to coding, we’re all newbies in something.

{% include twitter_plug.html %}