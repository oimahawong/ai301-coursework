# Procedure: how this skill grades a plan package

## Read order

1. Read the issue first: its title, body, and labels (eval: the
   `## Issue` section; live: the issue page). Note in one line what
   symptom was actually reported and under what conditions.
2. Read `## Repo facts` (eval) or gather the repo's bug-report
   template, contribution policy, and any stated AI-use disclosure
   requirement (live, per `references/evidence-guide.md`). Note
   whether an AI-disclosure requirement exists, since that gates the
   comms check later.
3. Read `## Thread highlights` (eval) or the live thread next. Note
   any explicit maintainer/owner direction: a named culprit file/line,
   an approach they proposed or rejected, a question they asked, a
   competing PR they linked. This has to be read before the plan,
   because judging whether the plan "engages the thread" requires
   knowing what the thread said independently of what the plan claims
   it said.
4. Read `## Repro evidence` next, before the candidate plan. Note
   every numbered step, every artifact (stack trace, timing number,
   rendered output), and every control run, and what each one
   establishes or rules out. Reading this before the plan prevents the
   plan's own framing of its diagnosis from anchoring what you think
   the evidence shows.
5. Only now read the candidate plan in full, then the candidate plan
   comment. Note the stated cause, the in-scope/not-in-scope line, the
   named files/approach, the test plan, and any stated risks or open
   questions.
6. Live mode only: read `scope.md` before grading anything (already
   required by `SKILL.md`) and `voice-guide.md` before the comms step.
   Eval mode: skip both; ignore them entirely.
7. Live mode only, when `plan.md` contains a filled `## Deviations`
   section: read it last, after the rest of the plan, since it may
   revise earlier claims.

## Evidence gathering

For each check, pull the specific fact from the specific place noted
during Read order; do not re-scan the whole package per check.

1. **diagnosis-grounded**: from step 4's notes, list every repro step
   and control run next to what the plan's stated cause (step 5) would
   predict for it. Record any mismatch verbatim (quote the control run
   and the cause).
2. **scope-bounded**: from step 5, pull the in-scope/not-in-scope line
   and the full approach list. Compare the approach list against the
   symptom noted in step 1 only — not against what would be nice to
   also fix.
3. **executable**: from step 5's approach, record whether a specific
   file/location is named and whether exactly one implementation route
   is chosen, quoting the line that commits (or fails to commit) to it.
4. **test-plan-decisive**: from step 5's test plan, record the named
   expected outcome verbatim; cross-reference it against step 4's repro
   steps to confirm it maps onto a real one.
5. **honest-about-unknowns**: from step 5, record every claim stated as
   fact and check each against step 4's repro evidence; separately
   record any stated risk/unknown and whether it reads as flagged
   (hedged) or asserted (confident). If `plan.md`'s `## Deviations` was
   read in step 7, record whether it has content and whether that
   content matches the real diff (live mode only; in eval mode there is
   no diff to check against, so grade only the claims-vs-evidence half).
6. **comms-thread-aware**: from step 2 and step 3's notes, check the
   plan comment (step 5) against the recorded maintainer direction and
   against the recorded AI-disclosure requirement. Record both checks
   separately even though they share one row: a pass requires both to
   hold.

## Check execution

1. Grade the six checks in the table order given in `rubric.md`:
   diagnosis-grounded, scope-bounded, executable, test-plan-decisive,
   honest-about-unknowns, comms-thread-aware.
2. Each check is graded once, from the evidence recorded for it in the
   Evidence gathering step above; do not re-read the full package per
   check.
3. Apply the check's pass condition from `rubric.md` literally to the
   recorded evidence. A check passes only if the recorded evidence
   satisfies the pass condition; it fails if the recorded evidence
   contradicts it.
4. Grade a check `unclear` only when the package genuinely gives no
   evidence either way for that check (for example: no stated test
   plan at all, rather than a vague one — a vague-but-present test plan
   is a `fail`, not `unclear`). Do not use `unclear` to avoid a close
   call the pass condition already decides.
5. For every check, write down the one fact or quote that decided the
   grade (the specific control run, the specific named file, the
   specific vague phrase) before moving to the next check. This is
   what goes in the output JSON's `evidence` field.
6. A check's grade never changes because another check already failed;
   grade all six independently, even once a reject looks certain, so
   the output JSON always reports a complete set of six grades.

## Verdict assembly

1. Apply `rubric.md`'s verdict rule: accept only if all six checks
   graded `pass`; any `fail` (or `unclear`, which this rubric treats as
   `fail`) on any check makes the verdict `reject`.
2. When the verdict is `reject`, the deciding check(s) for the summary
   are every check that graded `fail` or `unclear`, not just the first
   one found — list all of them, since a student revising the package
   needs to know every gap, not just the first.
3. Quote the exact evidence recorded for each deciding check in the
   summary (the same fact recorded in Evidence gathering), so the
   verdict is traceable back to a specific line in the package rather
   than a general impression.
4. Live mode only: after the six rubric checks are graded, separately
   check the plan comment against `voice-guide.md`'s rules and report
   any rule it breaks in the summary, quoting the rule. A broken voice
   rule is reported but never changes the accept/reject verdict, since
   the verdict space is defined entirely by `rubric.md`.
5. Emit the verdict and all six check grades in the fenced JSON block
   `SKILL.md` specifies, as the last thing in the output.
