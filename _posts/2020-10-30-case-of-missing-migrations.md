---
title: The Case of the Missing Migrations
permalink: /missing-migrations
date: 2020-10-30 18:00:00 +1100
tags: [inherited-codebase-diaries]
---

I've been working exclusively in an inherited codebase for nearly a year now and I frequently see things the previous developers did that have caused problems.

Everytime I see one of these, I joke to myself that I'm going to write a book called _The Inherited Codebase Diaries_.

I've just started a little freelancing on the side too, and have come up against the same problem I first experienced my normal day job codebase, so I can resist no more:

## The Inherited Codebase Diaries: The case of the missing migrations

Many database ORMs / App frameworks offer database migrations. These are like source code for your database.

The great thing about them is that regardless of changes to your database schema, you can roll it back to any point in its history and restore a working database.

It also allows new developers to spin up your app from scratch, run the database migrations, and then start developing.

In theory, for example, you can clone a git repo of a production Laravel app, run a few set up commands (such as migration) and then have a working dev environment in minutes.

### The problem

Unfortunately, it can be tempting to make ad hoc changes to your database schema on the fly by directly manipulating the database.

A little MySql command on the terminal or a 'right click and change data type on this field' in MySql Workbench is all it takes to change a VARCHAR to TEXT and it's much quicker and easier than writing the migration, but it now means the migration records have a hole in them.

This problem compounds when you do it multiple times, and the real problems start to kick in when later migrations make changes to the database as it is (hacky) but won't work against the database you should have (according to your pristine migration records).

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Laravel folks:<br>How bad is it that changes have been made to prod DB without migrations (col data type changed &amp; new col added to table)?<br>Can I fix this by writing and running the migrations they should have written, or will the migrations fail because the schema is out of sync?</p>&mdash; Jackson Bates (@JacksonBates) <a href="https://twitter.com/JacksonBates/status/1203074735531118592?ref_src=twsrc%5Etfw">December 6, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

### Fixing the problem

You can probably just write the missing migration and run it - this might work, if you're only dealing with a datatype change or column addition that is not later referenced by another migration.

This won't work if dependent migrations are an issue.

Another thing to try is to write the migration, but backdate it so it runs at a time it should have run (migrations run chronologically). In this instance you want to carefully review all the migrations that reference the table and field in question and ensure your change makes logical sense.

You'll also need to tell your prod copy of the database that this migration has already run - in Laravel, for example, you could do this by manually adding a record to the migration table. Obviously, this is dangerous - you're directly manipulating prod data. If it's feasible, dump the prod database locally and test the change on your machine before messing with the real deal.

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Depends if you want to be able to recreate the database from migrations at any point. I would write the migration then manually add the row to the migrations table. Just be careful if there are dependent migrations that have been added since</p>&mdash; Ben Slinger (@ben_slinger) <a href="https://twitter.com/ben_slinger/status/1203081773657116672?ref_src=twsrc%5Etfw">December 6, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

### Variations on the problem

The recent incarnation of this problem is more problematic.

Let's say you have an existing app with a database, and then you decide to rewrite it in Laravel.

The database already has a schema, and a long history of changes, but no migrations keeping record of that.

Migrations generated on top of that will then make reference to a whole host of tables that the migrations have no concept of. When your new dev comes on board in this instance, they cannot rebuild your database at all, or really even reason about the schema.

In this case, you likely have to provide them with a dump of your local database for them to work on - but this just kicks the problem down the road. In reality, you have no ability to spin up a fresh instance, and this will make testing and on-boarding a pain forevermore.

### Moral of the story

This ranges from minor to major pain in the ass, depending on the extent of the problem.

If you make any change to your database, you must do so with migrations that can depend on each other, without breaking that dependency chain with ad hoc amendments.

Also ensure your migrations are written properly to allow them to rollback accurately, too. Your ORM documentation will explain how.

{% include twitter_plug.html %}
