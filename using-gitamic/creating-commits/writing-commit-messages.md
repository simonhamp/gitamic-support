---
description: How to write clear and concise commit messages
---

# Writing commit messages

A lot of this page is inspired by and adapted from [this fantastic post](https://cbea.ms/git-commit/) by cbeams.

> A well-cared for log is a beautiful and useful thing.

> \[Good committers] know that a well-crafted Git commit message is the best way to communicate _context_ about a change to fellow developers (and indeed to their future selves)
>
> — [cbeams, 2014](https://cbea.ms/git-commit/)

These are some useful guidelines.

### Separate subject from body with a blank line

Not every commit requires both a subject _and_ a body. If the subject is enough, it's enough.

But when you do need to provide more detail, separate the subject from the body with a blank line.

```
Here's the subject

And here's the body that goes into a lot more detail.
```

### Limit the subject line to 50 characters

This isn't a rule, but it encourages you to be concise. It also means that the subject will be presented nicely in most places without being trimmed.

### Capitalize the subject line

Readability starts with first principles, but...

### Do not end the subject line with a period

Every character counts when you're being concise.

### Use the imperative mood in the subject line

Write like you're commanding someone to do something, not past tense expressing what you _did_.

### Use the body to explain _what_ and _why_ vs. how

This is possibly the most important recommendation. When committing many changes, you should focus on giving context on what has changed and why it was needed, and less on how.

For most content changes this probably won't be a major concern, but if your changes cover code, then the _how_ can be found by the person reading the changes in the commit history; what they can't see from the code is _why_.
