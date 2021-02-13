Purpose of this piece - to encourage curiosity, personal development, and thinking beyond your specialism.

The common way we think of web developers at the moment is as front-end, back-end, or full-stack developers. There has been some nuance introduced into these distinctions, such as whether one is a more focused on the new wave of JavaScript powered innovations (React, GraphQL etc), or focused on CSS, accessibility and UX, as per Chris Coyier's thought provoking piece from a couple of years ago: https://css-tricks.com/the-great-divide/. There's also been some additions to this, with the inclusion of DevOps, DevSecOps, and SREs. But true software engineering isn't so much about learning some frontend or backend languages, or some flavours of databases - it's about understanding complex systems.

The idea of a stack is comfortable because it's easy to think of all the parts of a system as layers: we have the server layer, and on top of that is the database layer and api layer, and on top of that is the frontend, UI layer, and on top of that is the CI layer, and then the deployment layer and so on.

But I'd argue that a neat stack is the wrong metaphor for visualising the work we do.

https://c.tenor.com/9b9cUZ-lse4AAAAM/spinning-plates.gif

In larger companies you may have the luxury of working on just one spinning plate - you might even be on a team that deals with one plate (although you should realise that a team is itself a number of plates that make up the system too).

At Grace Papers we're a 2 person dev team (and last year it was just me). So every plate has to be kept spinning by the two of us. At that point the front end, backend, full stack distinction becomes meaningless.

So to illustrate what a week overseeing the whole system looks like, here are the plates I can remember spinning recently:

- Amazon EC2 server maintainance, some Ubuntu, some 'Amazon Linux', via ssh
- SSL certificate update automation
- Amazon RDS database configuration and management
- DNS record changing
- Wordpress marketing site administration and migration
- Active development of 3 React codebases
- Active development of a Laraval PHP api codebase
- QA and testing automation
- Code review
- Developing and maintaining CI/CD pipelines
- Integration with 3rd party platforms like Hubspot
- Reverse engineering established 'no code' solutions that were handed over from consultants years ago and are no longer suitable.
- Meetings with external agencies around design, data strategy, cloud services, security, and marketing.

Some of this falls outside of the remit of what we think of as software development, but it's all relevant work - since the code we write either has an impact on these other areas, or is determined by those areas. This is especially true when it comes to integrations, because the system relies on its interconnectedness and interdependencies.

The plate spinning metaphor would be more accurate still if we could visualise many of those plates being tethered together somehow, like mountain climbers: when one falls, many more might come down with it.

Software engineering is about understanding systems - at the micro level or individual languages or parts or the stack, and at the macro level - how it all fits together.

None of this is mentioned to say 'You are not a Software Engineer unless you know how to do it all!'

Rather, I'd like to encourage you to consider perhaps a wider scope for your expertise than simply front-end, back-end, full-stack, CloudOps etc.

The other thing I'm hoping to encourage is a sense of curiosity in some less well known parts of the stack. 

So maybe you heard the part where I said I had to automate SSL certificate updates and your ears pricked up because you realised for the first time that it might actually be pretty cool to ssh onto a server and write a cron task to do something. It's actually not that cool, but it did save our company $400 a month, which is what Amazon charge for the same service. It's literally a couple of shell commands and a one line cron job though, so it's a really easy way to save money and win brownie points at work!

When you start to look in the little dark corners of your system and learn how to keep the lesser known plates spinning, you can become absolutely indispensible, especially in small companies.

While specialising can make it much easier to market yourself to big companies, being a competent generalist can help you identify the area you really want to specialise in eventually. If you've heard of the T-shaped developer, one with broad knowledge generally, and deep knowledge in one specific area, learning to keep a lot of the plates spinning is an important step in achieving that ideal.



