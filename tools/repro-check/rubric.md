# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment-recorded | The repro report's environment line(s): version of the software under test, OS/platform, and how it was installed/run. | Pass if the version and OS/platform are stated explicitly and specifically enough that someone else could set up the same box (e.g. "lazygit 0.64.1 (release binary), Ubuntu 24.04", not "my machine" or "latest"). Fail if no environment is stated at all, or if it names only some of version/OS and the missing piece matters for the issue (e.g. the issue is platform- or driver-specific and the platform or driver is never named). | required |
| Steps-followable | The exact commands/actions in the repro report, from starting state through to the observed output. | Pass if a stranger with the stated environment could re-run the same steps and land in the same state: every command and triggering condition the issue requires is given in the report itself (not referenced as living in a private repo, an unshared config, or "my setup"), and any input file's content is either shown verbatim or described precisely enough that the specific triggering element (the exact flag, field, or value that causes the bug) is fully pinned down, even if incidental details are paraphrased. Fail if the trigger depends on a resource the report does not share, if the steps skip the specific condition the issue says causes the bug (e.g. running a plain case instead of the boundary/edge case named in the issue), or if an input file is described too vaguely to pin down the triggering content. | required |
| Behavior-matches-issue | The artifact shown (output excerpt, exit code, log, screenshot) in the repro report, read against the specific mechanism/error/symptom the issue describes. | Pass if the artifact actually shows the behavior the issue names (same failure point, same error class, same symptom) — or, for a cannot-reproduce, the report shows a genuine attempt at the issue's specific trigger and says plainly it did not occur. If the tested input, command, or version differs from the issue's, pass only if the report says so and the artifact still bears on the issue's behavior. Fail if the artifact shows a different, adjacent outcome (e.g. a graceful validation error standing in for a reported crash, an old version's known behavior standing in for a bug confirmed on current/main) and the report narrates it as confirming the issue anyway. | required |
| Claims-evidenced | Every assertion of "this reproduces," "this is the cause," or "expected vs. actual" in the report, matched against the artifact actually shown. | Pass if each claim is backed by the artifact shown in the same report, including an honest, evidenced "I could not reproduce this" that shows the attempt. Fail if the report asserts success, certainty, or a root cause ("guaranteed reproducible," "I verified this race condition," "definitely the X bug") with no artifact shown to back it, or if "expected"/"actual" are stated in a way the shown artifact contradicts. | required |
| Comment-specific | The candidate claim comment's content: what issue it names, what it says it will do next. | Pass if the claim is specific to this issue (names the bug, states a concrete next step such as "test the draft patch" or "narrow the trigger") rather than interchangeable text that could be pasted onto any issue, and if it promises only investigation/next steps, not a guaranteed fix or delivery date. Fail if the comment is generic boilerplate ("+1, claiming this, will fix soon") or promises an outcome or timeline the author cannot back at this stage. | required |
| Disclosure-compliant | The repo-facts block's stated AI-use policy (if any), matched against whether the candidate claim comment and repro report disclose AI assistance. | Pass if the repo states no AI-disclosure requirement, or states one and the comments disclose the tool and extent of AI assistance as asked. Fail only if the repo's stated policy requires disclosure and neither candidate comment discloses it. | required |
| Minimal-and-isolated | Whether the repro report isolates the trigger (a control/comparison run, or a reduced case) rather than just narrating one run. | Pass if the report includes a control run, a minimal reduction, or an explicit comparison that isolates what causes the behavior. This never changes the verdict; it is a quality signal, not a gate. | preferred |

## Verdict rule

Accept only if every `required` check above grades `pass`. A single
`required` check graded `fail` or `unclear` makes the verdict `reject`;
`unclear` is treated as `fail` throughout, since proof that cannot be
verified is proof that is not ready to post. `preferred` checks
(Minimal-and-isolated) are reported but never flip the verdict either
way.
