# The Plate Spinning Developer, understanding the roles and responsibilities of a Software Engineer

When I was starting out as a Junior Developer it was common to hear the profession of web development being split into 3 broad categories or specialisms - and it's still the prevailing way most of us think about our responsibilities. The common way we think of web developers at the moment is as front-end, back-end, or full-stack developers. There has been some nuance introduced into these distinctions, such as whether one is a more focused on the new wave of JavaScript powered innovations (React, GraphQL etc), or focused on CSS, accessibility and UX, as per Chris Coyier's thought provoking piece from a couple of years ago: https://css-tricks.com/the-great-divide/. There's also been some additions to this, with the inclusion of DevOps, DevSecOps, and Site Reliability Engineering (SREs). This categorisation can be useful when determining who on a team has responsibility for particular types of issue or work. It can also be useful for beginners as it segments an almost infinite number of things one can learn, into smaller groups so it's easier to make decisions about what to learn next and what an appropriate path towards your specific goals might be.

But true software engineering isn't so much about learning some frontend or backend languages, or some flavours of databases, and leaving the rest alone. Software engineering is about understanding complex systems.

The idea of a stack is comfortable because it's easy to think of all the parts of a system as layers: we have the server layer, and on top of that is the database layer and api layer, and on top of that is the frontend, UI layer, and on top of that is the CI layer, and then the deployment layer and so on.

But I'd argue that a neat stack is the wrong metaphor for visualising the work we do.

https://c.tenor.com/9b9cUZ-lse4AAAAM/spinning-plates.gif

In larger companies you may have the luxury of working on just one spinning plate - you might even be on a team that deals with one plate - and it could be something as specific as a single customer facing feature within a much larger product. Even if you are on a team working on a single thing, you should realise that a team is itself a number of plates that make up the system too. People add just as much complexity as technology, and often much more!

At Grace Papers we're a 2 person dev team (and last year it was just me). So every plate has to be kept spinning by the two of us. At that point the front end / back end / full stack distinction becomes meaningless.

So to illustrate what a week overseeing the whole system looks like, here are the plates I can remember spinning recently:

- Active development of 3 React codebases
- Wordpress marketing site administration and migration
- Active development of a Laraval PHP api codebase
- Integration with 3rd party platforms like Hubspot
- Reverse engineering established 'no code' solutions that were handed over from consultants years ago and are no longer suitable.
- Remote database configuration and management
- Server maintainance, with multiple operating systems, via ssh acces
- Automating the update of security certificates (SSL)
- Changing DNS records (i.e. the resources web addresses point at)
- Quality Assurance and testing automation
- Developing and maintaining CI/CD pipelines (i.e. changing how deployments are handled, automatically)
- Code review
- Meetings with external agencies around design, data strategy, cloud services, security, and marketing.

Some of this falls outside of the remit of what we think of as software development, but it's all relevant work - since the code we write either has an impact on these other areas, or is determined by those areas. This is especially true when it comes to integrations, because the system relies on its interconnectedness and interdependencies.

The plate spinning metaphor would be more accurate still if we could visualise many of those plates being tethered together somehow, like mountain climbers: when one falls, many more might come down with it.

Now if we were a larger team, much of this might fall to other team members - those at the top of the list would be the frontender's jobs, next on the list would be for the backend, then the devops folks, then the QA folks, and maybe the project manager at the end. Even if a single person isn't doing all of those things, it is useful for a software engineer to understand that these are some of the parts of the larger system they are working within.

One of the quickest ways to level up as a developer is to find the people that have these other responsibilities and learn from them to have a better understanding of what they do.

Software engineering is about understanding systems - at the micro level or individual languages or parts or the stack, and at the macro level - how it all fits together.

None of this is mentioned to say 'You are not a Software Engineer unless you know how to do it all!'

Rather, I'd like to encourage you to consider perhaps a wider scope for your expertise than simply front-end, back-end, full-stack, CloudOps etc.

The other thing I'm hoping to encourage is a sense of curiosity in some less well known parts of the stack.

So maybe you noticed in the list above the part where I said I had to automate SSL certificate updates. This is achieved by connecting via ssh in your terminal to your remote server and writing a cron task that performs a scheduled update of the certificate. And for some of you, that might catch your attention because you realised for the first time that it might actually be pretty cool to remotely connect to a server and write a script to do something important for security. It's actually not that cool, but in this instance it did save our company $400 a month, which is what Amazon charge for the same service. It's literally a couple of shell commands and a one line cron job though, so it's a really easy way to save money and win brownie points at work!

When you start to look in the little dark corners of your system and learn how to keep the lesser known plates spinning, you can become absolutely indispensible, especially in small companies.

While specialising can make it much easier to market yourself to big companies, being a competent generalist can help you identify the area you really want to specialise in eventually. I strongly dislike the idea of a 10x developer that you may hear from time to time on Twitter and Hacker News, but I am quite taken with the idea that it describes someone that can keep 10 plates spinning at a time. If you've heard of the T-shaped developer, one with broad knowledge generally, and deep knowledge in one specific area, learning to keep a lot of the plates spinning is an important step in achieving that ideal. That said, this should be considered a more intermediate goal! It's totally fine and advisable to focus on one thing at a time, especially when you are in the very early stages of your career or developer journey.
