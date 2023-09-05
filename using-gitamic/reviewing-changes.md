---
description: How to use Gitamic to review your work
---

# ☑ Reviewing changes

The Gitamic work area is divided into two main sections: **Unstaged** and **Staged**. You can see at a glance how many files are in each work area, so you can easily see where your attention is needed.

<figure><img src="../.gitbook/assets/Screenshot 2023-09-04 at 22.25.32.png" alt=""><figcaption><p>Wow! There are 4 changes already</p></figcaption></figure>

### Unstaged files

Start in the **Unstaged** tab. Here you can see all files with changes that Git has identified.

Clicking on a file's path in the list will open the Diff viewer, allowing you to see all of the unstaged changes made to each file. (If you have any _staged_ changes in this file, you will need to view the file'ss diff from the **Staged** tab.)

You can stage one file at a time by clicking on the context menu to the right of each file (...) and selecting `Stage`.

<figure><img src="../.gitbook/assets/Screenshot 2023-09-04 at 22.04.32.png" alt=""><figcaption><p>Click 'Staged' to mark all changes in this file as ready to be committed</p></figcaption></figure>

`Discard` erases the changes - so if the changes modify the file in any way, discarding them will reverse those changes: new content will be erased, deleted content will be restored.

You can stage many files at once using the bulk action checkboxes. Simply check one of the boxes to the left of each file and the bulk action options will appear at the top.

<figure><img src="../.gitbook/assets/Screenshot 2023-09-04 at 22.06.39.png" alt=""><figcaption><p>Bulk actions make it easy to move through lots of changes rapidly</p></figcaption></figure>

It's useful to review the changes of each file and only stage what you know you want to commit. You can leave any changes that you don't want to commit in the _unstaged_ state – Git will only commit changes that are _staged_.

### Staged files

In the **Staged** tab you can see all of the files with changes that you have _staged_, or marked as ready to be committed.

You can view the diffs of staged changes by clicking on the file path.

You can unstage a whole file from the context menu by clicking `Unstage`. These changes will now appear in the file's **Unstaged** view again.

You can bulk unstage many files at once.

### Viewing diffs

<figure><img src="../.gitbook/assets/Screenshot 2023-09-04 at 22.35.34.png" alt=""><figcaption><p>Gitamic's diff viewer is powerful ⚡️</p></figcaption></figure>

The **Diff viewer** is a critical part of reviewing changes made to your files. It shows you quickly what's changed and lets you decide which _parts_ of a file you want to commit.

Let's break down the diff viewer.

When viewing diffs from files in the **Staged** or **Unstaged** tabs, you will see the changes for just _one file_. So you will see only one file card in the diff viewer, with the file name at the top of the card.

This also gives you a summary of the changes - an indicator of the type of change (the one above is an <mark style="background-color:green;">A</mark>ddition) and how many chunks have been detected. In this case, this whole file is new, so there's just one chunk.

It looks like a new entry in the `posts` collection!

Then there's the numbers in the left-hand column and the text on the right-hand side.

The numbers are the line numbers in the file. This can make it easier to find the changes in a code editor or other tools.

There are two banks of line numbers side-by-side: the left bank shows the numbers in the file _before_ the change, the right shows the numbers _after_ the change. In this example, there is no left bank as the file is completely new.

The diff viewer shows _blended_ diffs where both versions of the file are shown together. This can sometimes be aid with spotting exactly what has changed in a specific chunk.

The text in the big right-hand column should be obvious: this is the contents of the file. Sometimes it will show the entire file. At other times it will show just some snippets of the file (called **Chunks**).

Each chunk is collapsible (useful when there are many chunks) and can be staged/unstaged independently of other changes. See [#patching-chunks](reviewing-changes.md#patching-chunks "mention")for more.

You can use the `Context lines` setting to adjust how many lines of context are shown next to each chunk (click `Refresh` to see the change). Depending on the size of the file, this may affect the number of chunks.

#### Diffs

The diffs themselves are generally made up of three parts:

* **Old lines** show how the file appeared before any changes were made, according to Git's [#index](git-basics.md#index "mention"). They appear in <mark style="background-color:red;">red</mark> and indicate that this line has changed or been removed entirely.
* **New lines** show the _current state of the file_. They appear in <mark style="background-color:green;">green</mark> and indicate that this line contains something new or different to what was there previously.
* **Context lines** may or may not appear depending on the state of the file – completely new files or deleted files won't have any context, for example, because the whole file has changed. When they do appear, they have the default background color.

You can `Stage all` or `Unstage all` (depending on where you viewed the diff from – the **Staged** or **Unstaged** tab), using the blue button at the top of the file card.

#### Patching chunks

With Gitamic, you can stage or unstage individual chunks. Simply use the `Stage` or `Unstage` button at the top-right of a chunk to move it from one part of the working tree to another.

Once a chunk's status has changed, it will disappear from the current view as you will be viewing a different context. For example, if you're viewing an unstaged file with 3 chunks and you stage one chunk, you will now see only 2 chunks.

This provides for a nice visual workflow.

When all chunks have been moved into the other context, the context will shift automatically to show you the fully staged or unstaged file and you should see all of the chunks re-appear.

{% hint style="warning" %}
**Remember:** _Everything_ in a chunk gets staged or unstaged together. If you want to increase/decrease how much is included in a chunk, change the `Context lines` setting.
{% endhint %}

{% embed url="https://youtu.be/b-c-q0LngMc" %}
See chunk patching in action
{% endembed %}
