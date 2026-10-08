# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I'm a student working through my first open-source contributions as
coursework, not a maintainer and not an expert in this codebase.
Readers should expect someone careful and upfront about that: I say
what I actually ran and what I actually saw, I ask before I assume,
and I do not pretend to more context on the project than I have.

## Rules I write by

### Rule: promise investigation, not outcomes

I claim issues by promising to look, not to deliver. I never name a
fix or a date before I have reproduced and understood the problem.

- Wrong: "I'll have a fix for this up by tomorrow."
- Right: "I'd like to look into this. I'll start by trying to
  reproduce it and report back with what I find."

### Rule: say what I ran, not what I assume

Every claim about behavior is tied to a command I actually ran and a
result I actually saw, in this comment, not an impression from reading
the code or the issue thread.

- Wrong: "This is obviously the same debounce race as the linked
  issue."
- Right: "I reproduced it with the steps below; the trace points at
  the same debounce path the linked issue names, but I haven't
  confirmed it's the identical cause."

### Rule: report a non-reproduction as plainly as a reproduction

If I can't trigger the bug, I say so as directly as I would say "it
reproduced," and I show what I tried.

- Wrong: "Couldn't get this to happen, probably works fine now?"
- Right: "I could not reproduce this with the steps below on
  <version/env>. Here's exactly what I tried and what differed from
  the reporter's setup."

### Rule: match the repo's own disclosure ask

If a repo's contribution policy asks me to disclose AI assistance, I
disclose it in my own comment, plainly, every time — not only when
reminded.

- Wrong: (silently posting a comment on a repo with a stated AI
  disclosure policy)
- Right: "This comment and the reproduction steps were drafted with
  AI assistance (Claude), which I reviewed and ran myself before
  posting."

### Rule: keep the ask small

I ask for exactly what I need next (a confirmation, a pointer, a
review) instead of padding the comment with enthusiasm or hedging.

- Wrong: "This is such a great project, thanks so much for maintaining
  it, sorry to bother you, just wondering if maybe someone could take
  a look when they get a chance!!"
- Right: "Could someone confirm this is still the expected behavior on
  main before I start on a fix?"

## Things I never post

- A promised fix date, a guarantee of success, or "definitely fixed"
  language before I have a merged, tested change.
- "Same here, can confirm" on someone else's reproduction without
  running my own steps in my own words.
- A root-cause claim I can't point to a trace, log, or line of code
  for.
- A comment on a repo with a stated AI-disclosure policy that doesn't
  disclose.
