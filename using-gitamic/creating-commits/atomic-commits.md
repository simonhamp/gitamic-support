---
description: It's a good practice to make them atomic
---

# Atomic commits

### What's an atomic commit?

Atomic commits are self-contained and "complete" in the sense that the changes they record work together as a single unit.

If you ever need to reverse (known as a 'revert' in Git lingo) some work, you will find it much easier if many changes that are related to each other (or even depend on each other) are clumped together in a single revision.

{% hint style="info" %}
This is one of the most important reasons for creating manual commits rather than leaving it to an automated process: **you cannot achieve true atomic commits when many changes are automatically rolled up into commits.**
{% endhint %}

Practicing atomic commits also has the side-effect of encouraging smaller sets of changes that can more easily be rolled up together, which helps to bring focus to your work, allowing you to move more quickly.

If you think in terms of jobs to be done, you can think of a commit as the completion of a job: the contents of the commit (the changeset) should represent everything needed to complete that task.

This also leads to your jobs/tasks reaching a useful level of granularity. For example, instead of a task called "Improve homepage CTA" which might incorporate a bundle of small jobs in your project management tool of choice, you end up with discrete tasks for things like "Change 'Join now' to 'Sign up today!' on homepage" because you know this is a clear and concise piece of work.

That, in turn, makes deciding what your commit message should be that much easier – you (or someone else) already wrote it!

And it's far easier to find a commit message that has the name of the task as the heading than it is to search based on any other criteria. Your project management tool may even be able to make the connection between your tasks and your commits automatically for you.

**A virtuous circle!**

### The case for manual commits - an example

{% hint style="danger" %}
This scenario is based on real events that occurred on a Statamic site I built and managed for 5 years.

The team editing it was small - no more than 5 people - and we used Statamic v2 with the Spock add-on, which was the precursor to Statamic's now built-in Git Automation.

We bumped into these kinds of problems almost every week.
{% endhint %}

You made some edits to the homepage of a client site that you help to manage - these changes need to be live today, but because you've used Statamic it's only going to take you a few minutes.

Meanwhile, your client - let's call them Jen - has made a whole bunch of complex edits on a number of different landing pages, some of which were saved a short time from when you made your changes to the homepage.

For getting the work done, this should all be fine. There's no conflicts as Statamic lets you both work on separate pieces of content at the same time without any trouble.

With auto-commits, neither of you have to think about staging or committing any work - all the work done gets committed and pushed to the repo, job done.

A little while later, Jen calls you. It turns out all of the changes they made weren't meant to go live yet and they need to revert all of that work. They could do it manually, but they know you can do it quicker with your software wizardry 🧙 🪄

You check the commit history to see what the damage is, but sadly it's a bit of a mess.

It looks like your changes have been wrapped up with some of Jen's changes into one commit and then there are a few more commits covering a hopscotch of Jen's changes over the course of an hour or so that they were working on the site.

Oh dear!

What you want here is a **single commit** for each set of changes: one that captures just the changes Jen made and one that captures just your changes. Then you could easily roll back only Jen's changes using Git's revert feature.

(Failing that, even a commit for each individual file that was changed would be ok as you could work them all out and do them all one by one.)

Unfortunately you have neither in this world of automatic commits: your homepage changes will get reverted along with all of Jen's changes, meaning that, no matter which way you cut it, there's going to be more manual work here for you than you'd like.

It might still be less than Jen would have to do and it's not like your work is lost - it is recorded in Git after all - but it's grunt work nonetheless and you've got more interesting work you could be doing.

Your short and sweet content update task has now turned into an urgent and time-consuming Git management nightmare.

**This is where manual, atomic commits can save you!**

Granted, this might not happen very often and it's a trade-off - some time spent each time you do some work to think carefully about what's been done and how it should be organised in the repo's history versus potentially spending an extra hour here and there cleaning up some messy revert.

But as soon as more people start making edits to this site, these kinds of headaches become far more frequent... and far messier.

Getting everyone into the good practice of creating manual, atomic commits, however, allows you all to individually decide which parts of the work that you've done can be grouped together into appropriate revisions in the repo's history.

Then, should you ever need to revert a whole chunk of work, it is just a single, clean commit away.
