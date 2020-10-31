---
title: The Case of the Spontaneous Data
permalink: /spontaneous-data
date: 2020-10-31 11:00:00 +1100
tags: [inherited-codebase-diaries, laravel, databases]
---

Long before the invention of the internet, and indeed before medecine as we know it, there was a belief in a process known as Spontaneous Generation.

It was the explanation for the manifestation of maggots on meat left exposed for a time. It was the explanation for the appearance of mice in pantries where cheese had been left. It might sometimes even tempt you to believe that the bugs in your code simply materialized, perhaps catalyzed by the proximity of your code, but certainly not caused by it.

## The Inherited Codebase Diaries: The case of the spontaneous data

The previous blog post discussed the virtues of using database migrations to make and track changes to your database schema. We laughed, we cried, we prommised to never change our schemas without migrations ever again.

An interesting problem surfaced in the inherited codebase a few months ago.

I was writing some database seeders to set the stage for some automated testing (there were none, further chapters of these diaries are indeed pending). One of the seeders was recreating some user roles. For argument's sake let's say `id = 4` was for **Wizard** and `id = 5` was for **Ninja**.

Running the completely fresh migrations and seeding the entirely empty database threw an error.

Allegedly `roles.id` 5 and 6 already existed! They had somehow spontaneously generated!

Louis Pasteur proved spontaneous generation was an insufficient theory to explain the replication of bacteria, and a careful look in your inherited codebase may reveal similar scientific truths to you.

### The culprit

As wonderful and important as database migrations are, you shouldn't use your migrations to make every change to your database. While the structure of the database is crucial, what would your database be without the data? As important as it is to have good data, you should not be committing your data to migrations - even though this is possible and seems to make sense on the surface.

In this instance, the errant Wizard and Ninja in the database were not merely appearing, they had been specifically added in the roles table as part of a migration performed on it.

It's worth pointing out that IDs 1-4 and 7+ were not handled in migrations, just these two.

One does not simply expect consistency in an inherited codebase.

### The solution

What should they have done instead?

If you need to seed a database with some initial values, it is likely your framework or ORM has the ability to write seeders of some sort - just like I was doing with Laravel in setting up a test database.

You might find that you need to migrate data in your prod database - either reformating data in bulk, or adding new data in an automated way. In this case you likely have another scripting solution provided by your framework. For example Laravel has Artisan commands and Rails has Rake tasks. These can be a great tool for one off changes to your data in your database.

The benefit of seeders is that they assume a clean slate. The benefit of artisan or rake tasks is that they can assume an occupied database and be as bespoke as you need them to be for large scale operations.

The downside of handling these use cases with migrations is that the migrations alone can't make assumptions based on the existing data, and applying data migrations on one occupied database can behave differently to others.

Of course, the real culprit here is the inconsistency! One developer deciding to adopt a completely different pattern to the rest of their team, and then having that pass code review and make into production is sloppy to say the least. It is, however, not the most egregious thing I've seen in the inherited codebase so far...

{% include twitter_plug.html %}
