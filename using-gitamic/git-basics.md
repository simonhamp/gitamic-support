---
description: A brief introduction to some basic Git concepts
---

# ℹ Git basics

Git is probably the most popular source code/version control software available on the planet. And for good reason! It's a mature, robust, and reliable way to work collaboratively through a distributed system of maintaining file change history... and so much more.

This allows you to track changes to files over time, seeing how they changed, when they changed, and who made those changes. This makes it especially powerful for auditing and review! If used well, Git can help you:

* Review your own work, or someone else's, before merging it
* Run multiple streams of work concurrently
* Find when a bug was introduced into a codebase
* See who wrote that beautiful paragraph
* Quickly see the changes made between distant versions of multiple files

This is very useful in a number of highly-specific contexts – Git was created to make building Linux more manageable, so it's particularly great if you're building software/writing code – but in general it's great for managing changes to any sort of text file.

This is great in the context of Statamic when used as a flat-file CMS, as it enables some very powerful workflows!

This guide assumes you're familiar with Git to some degree (what it is and why it's used) and that you've already got Git installed on the relevant systems.

What we're going to cover here are just some of the basic concepts that Gitamic features expose. If you want to go into more detail about Git, check out the [Resources](git-basics.md#resources) section at the bottom of this page.

### Repository

A Git **Repository** (or 'repo' for short) is a combination of a Git database and all of the files included in it. This can be thought of most simply as the folder which contains your Statamic site.

Each repository has a special `.git` folder (usually hidden) within it – this is the Git database. Usually, the repository includes all files in the same directory as this `.git` directory, and all directories below it.

{% hint style="success" %}
**You don't need a Git repository to get started with Gitamic!** If your site isn't part of a Git repo, Gitamic will detect that and suggest some ways to get started.
{% endhint %}

### Revisions

A revision is a reference to a Git object. [#commits](git-basics.md#commits "mention") are a type of revision.

Each revision will have some form of absolute or relative identifier, e.g. a commit hash.

### Branches

**Branches** are an important concept in Git. Branches are offshoots, alternative timelines, of your project. They are lightweight and easy to create and destroy.

Gitamic doesn't currently support creating or managing branches, but this will change in the future.

It does show you which branch you're currently running and the remote branch that the branch you're working on is tracking. See [#remotes](git-basics.md#remotes "mention") below for more details.

### Merging

Coming soon!

#### Conflicts

### Working tree

The **Working tree** represents all the _differences_ between the [#index](git-basics.md#index "mention") and the current state of the file system.

The working tree is divided into a few states:

* **Untracked** - files which Git knows nothing about.\
  These are files that have not yet been added to the Index.
* **Unstaged** - files with changes that are _not ready_ to be committed.\
  These are files that exist in Git's index, but changes have been made to them and Git is allowing you the opportunity to review those changes.
* **Staged** - files with changes that _are_ ready to be committed.\
  These are files that exist in Git's index and have changes that you have staged ready to be committed, but they are not committed yet.

Gitamic simply splits these into two: **Unstaged** and **Staged**. Untracked files are part of the Unstaged list.

Changes listed in either of these sections have **not** been recorded in Git's [#index](git-basics.md#index "mention") so there is no revision for them.

#### Staging/unstaging changes

Files in the working tree can usually be moved freely between a staged and unstaged state.

### Index

The **Index** is Git's database, its record of changes that have been made. This is what enables Git to identify when changes are made, because it knows what the state of each tracked file should be.

#### Ignored files

It is possible to ignore files so that Git doesn't keep on alerting you to the fact that you have unresolved changes in them by adding a `.gitignore` file to the root of your project.

To ignore a file, simply add it's path on a new line in this `.gitignore` file.

```
.DS_Store
/.idea
```

See the [gitignore documentation](https://git-scm.com/docs/gitignore) for more details.

The `.gitignore` file itself will show up as a change that you will likely wish to commit so that it can be shared with collaborators or deployed to your servers.

### Diffs

Diffs are a comparison of two or more revisions of a given file. This allows you to see the difference between the revisions as represented by a diff view.

The diff view presents an algorithmically-calculated set of lines that Git believes to be different, often presenting changes contextually.

This makes for a convenient and reliable way to review what has changed:

{% content-ref url="reviewing-changes.md" %}
[reviewing-changes.md](reviewing-changes.md)
{% endcontent-ref %}

### Commits

**Commits** represent a moment in time. Each commit records a set of file changes (aka a changeset).

A commit can be made for changes of any size – either as little as a single character on one line in one file, or many hundreds of thousands of changes in thousands of files (though you should avoid making very large commits like this).

Each commit includes some metadata about the changes:

* when they occurred
* who made them
* a message written about the commits
* what commits came before this one
* a commit hash

The **commit hash** effectively makes the Git history immutable, which is an important feature if you want to guarantee that what happened according to the log is indeed how it was originally recorded.

{% hint style="success" %}
You can see the 20 most recent commits in Gitamic's **History** tab.
{% endhint %}

Now go see how to create commits in Gitamic:

{% content-ref url="creating-commits/" %}
[creating-commits](creating-commits/)
{% endcontent-ref %}

#### Commit messages

Writing clear and concise commit messages is an important skill that will serve you well later on. [Read my quick guide](creating-commits/writing-commit-messages.md) on how to do it well.

### Remotes

Git is a _distributed_ version control system and it encourages local-first revision control. When you need to share your changes with someone else (or deploy them to a server), you will need to set up a **Remote**.

Remotes are a kind of branch (see [#branches](git-basics.md#branches "mention")). If the other version of this repository (the remote) is using a branch that started off the same as the one you're using, they can diverge and eventually be merged back together.

This allows two instances of the same repository to communicate with each other and determine which commits each is missing. Git can then work out if it's possible to merge the commits from a given remote branch into your local branch.

{% hint style="info" %}
#### A word about '**local'** branches

By 'local' I mean 'local to wherever you're accessing your Statamic CP'. This may be on your own computer if you have your repository installed, e.g. if you're the website developer.

However, if you're editing your website online (e.g. at https://abcwidgets.com/cp), then the 'local' branch is most likely on a server somewhere on the Internet.
{% endhint %}

#### Tracking

Tracking remote branches allows Git to automatically compare the local branch to a known remote branch without having to define which branch to compare to every time.

This is like saying "I always want to keep my branch up to date with that branch on the remote end". Git can then allow you to push and pull changes more easily.

{% hint style="danger" %}
Gitamic doesn't yet allow you to manage remotes or set up branch tracking, but it's on the [roadmap.md](../roadmap.md "mention")!
{% endhint %}

#### Pushing & pulling

When you want to send new commits to a tracked remote branch (commits that it doesn't yet have), Git will identify that your branch is "ahead" and will allow you to **Push** the changes to the remote.

When the tracked remote branch has commits that your local branch doesn't have, Git will see that your branch is "behind" and will allow you to **Pull** the changes from the remote.

In some cases, your local branch can be _both ahead and behind_. In those cases, you MUST _pull first_, allowing Git to merge the remote changes into your local branch. Once that's done, you can push all your new commits.

This protects the remote from receiving commits that it can't merge, which would leave it in a messy state (not something you'd want on your production server!)

Now why not try pushing and pulling yourself?

{% content-ref url="pushing-and-pulling.md" %}
[pushing-and-pulling.md](pushing-and-pulling.md)
{% endcontent-ref %}

***

<details>

<summary>Resources</summary>

* [The official Git website](https://git-scm.com/)
* [gitignore documentation](https://git-scm.com/docs/gitignore)
* [GitHub's Getting started with Git](https://docs.github.com/en/get-started/getting-started-with-git)

</details>
