---
title: Overcoming a Gitlab Pipeline Failure
permalink: /gitlab-pipeline-failure
date: 2018-11-19 11:33:00 +0800
tags: [gitlab]
---

I ran into a weird issue during a Gitlab Merge Request today.

After submitting my Merge Request, the maintainer handling the merge had a warning:

> Could not retreive pipeline status.

Gitlab directs you to some documentation that gives two possible causes, but neither of these were relevant in our case.

## What was happening?

We had originally limited our CI pipeline to only run on the master branch, but due to a small error in an earlier update to our .gitlab-ci.yml, we had inadvertently opened these up to all commits on all branches.

In fixing this on the branch that was being merged, Gitlab was now in a state where it was previously getting CI status updates, but we had now told it to stop doing CI on that branch.

Gitlab doesn't like this and assumes no longer being able to test the branch is a bug, not a feature you intended.

## Fix

Once we determined this, the fix was easy: create a new branch from the old one and push that gitlab for the PR instead.

This means CI has never run on the branch, and it can be merged without complaints.

{% include twitter_plug.html %}