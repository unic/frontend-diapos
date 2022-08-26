---
title: Conventional Comments for Code Reviews
date: 26.08.2022
author: Manuel Lieb
confName: FrontConference
description: How to improve your communication, reduce misunderstandings and make your Reviewer life easier.
separator: "^\r?\n---\r?\n$"
verticalSeparator: "^\r?\n   ---\r?\n$"
theme: black
css: ./custom/styles/general.css
template: ./custom/templates/conference.html
highlightTheme: monokai
---

## Conventional Comments for Code Reviews

How to improve your communication, reduce misunderstandings and make your Reviewer life easier.

---

## Story Time 🔮

---

### The Cycle of Feelings in a Code Reviews

🙂 🤨 😟 😫 😵 🙈 🤦🏻‍♂️
<!-- .element: style="font-size: 5rem" -->

Restart the cycle on the next day ...
<!-- .element: class="fragment" -->

---

### We already use Conventions in the Repo

- Branch Names Prefixes
  - `feature/`, `bugfix/`, `release/`, ...
- Commit Tags
  - [Task], [New Feature], [Cleanup], ...

---

### How to use Conventional Comments

Start using a new Format Convention for your comments

```
<label> [decorations]: <subject>

[discussion]
```
<!-- .element: class="fragment" -->

   ---

#### Labels:
- suggestion
- question
- nitpick (nit)
- ...

   ---

#### Decorations:
- (blocking)
- (non-blocking)
- ...

   ---

#### Examples:

![Examples for Conventional Comments](assets/20220826/examples.png)

---

### Recap

Conventional Comments: 
- add more context to your comment
<!-- .element: class="fragment" -->
- help to minimize misunderstandings
<!-- .element: class="fragment" -->
- introduce a mental stopper for yourself - How do you Label your comment?
<!-- .element: class="fragment" -->

---

### Thank you

See more here: https://conventionalcomments.org/ and Kudos to Paul Slaughter
