# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: in an eval bundle, the opening lines of the "Candidate
repro report" section (usually labeled "Environment:" or similar). In
live mode, the student's draft report itself, plus the issue body and
its "Repo facts" bug-report template (which names what the maintainers
ask reporters to state — version, OS, how installed) so you know what
"sufficient" means for this repo.

What good looks like: the software's version (not "latest"), the OS or
platform, and how it was installed/run, stated as concrete values
someone else could match. When the issue is tied to a specific
platform, driver, or build profile (e.g. a Windows-only bug, a
debug-vs-release difference), the environment record names that
specific piece, not just "I tried it and it happened." A report that
tests a different version than the issue names it explicitly ("issue
filed against 4.53.2; I tested 4.53.3") rather than leaving the
version delta for the reader to notice.

## Steps

Where it lives: the "Steps" / "Preparation" / "Execution" portion of
the candidate repro report — the literal commands, inputs, or UI
actions, in order, from a clean starting state to the observed result.

What good looks like: every command needed to reach the failure is
shown in the report itself, not pointed at ("see my repo", "same
config as always") or left in an environment the reader cannot access
(a private monorepo, an unshared config file). An input file can be
shown verbatim or described in prose, as long as the description pins
down the exact triggering element (e.g. "a `category:` section the
schema doesn't recognize" is specific enough even without pasting the
whole YAML file; "a config similar to my usual setup" is not). The
steps include whatever specific condition the issue says triggers the
bug (an edge value, a flag combination, a file-size threshold) — not
just a plausible-looking but easier version of the scenario.

## Behavior shown

Where it lives: the artifact block in the candidate repro report
(terminal output, exit code, log excerpt, panic/backtrace, screenshot
description) and the "Expected"/"Actual" lines if present. Read these
against the issue's own description of the bug (its title, body, and
any quoted error/behavior) and, in eval mode, the repo-facts block if
it adds relevant context.

What good looks like: the artifact displays the same failure — same
error type, same exit behavior, same observable symptom — that the
issue names, not a different error produced by a changed input,
changed flag, or changed version. A changed command, operator, or
input value that produces a different (often more graceful) failure
than the one reported is a mismatch even when the report's prose
calls it a match. An honest "I could not trigger it" with a real
attempt and artifact shown still counts as showing the behavior
faithfully — absence of the bug, honestly demonstrated, is not the
same failure as absence of evidence.

## Honesty

Where it lives: compare every claim sentence in the claim comment and
repro report ("this reproduces," "confirmed," "the cause is," "this is
definitely X") against the artifact block that is supposed to back it.

What good looks like: a report that says exactly what was run and
exactly what came back, including when that means "I did not see the
bug." Warning signs: confident language ("guaranteed reproducible," "I
verified this race condition," emphatic repetition) with no command
output, trace, or artifact anywhere in the report; an "expected" or
"actual" line that contradicts what the shown artifact actually says;
a root cause asserted with no code or trace pointing to it.

## Comms

Where it lives: the candidate claim comment's own text, read against
the issue it names; and, for disclosure, the repo-facts block's
contribution-policy / AI-policy line (eval mode) or the repo's actual
CONTRIBUTING.md / AI-policy doc (live mode, per `references` the
scope.md and evidence-guide point you to).

What good looks like, specificity: the claim names the actual issue
and a concrete next step ("test the draft patch," "narrow the
trigger," "look at `decoder_hcl.go`"), not interchangeable text that
would read the same pasted onto any issue, and it promises
investigation only — never a guaranteed fix or a delivery date.

What good looks like, disclosure: when the repo's stated policy
requires disclosing AI assistance (tool used, extent of help), the
claim comment or repro report says so in plain words. A repo with no
stated AI policy, or a permissive one, has nothing to disclose and
this check passes by default. A strict, explicit disclosure
requirement with silence in both candidate comments is the one
condition that fails this check.
