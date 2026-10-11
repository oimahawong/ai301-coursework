# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's stated cause, read against every step, artifact, and control run in the repro evidence. | Pass if the stated cause explains every step/control run in the repro evidence and no step contradicts it. Fail if any step or control run in the repro evidence (especially a control that isolates or rules something out) contradicts, is ignored by, or is left unexplained by the stated cause. | required |
| scope-bounded | The plan's in-scope/not-in-scope statement and its approach, read against the symptom the issue and repro evidence actually describe. | Pass if the approach is confined to what fixing the reported symptom requires, with an explicit not-in-scope line (or equivalent deferral) excluding adjacent rewrites, migrations, new options/features, or module restructuring. Fail if the approach bundles the fix with a redesign, a cross-cutting migration, a new feature, or a rewrite of code not needed to address the symptom, even when the core fix inside it is correct. | required |
| executable | The plan's approach: named file(s)/location(s) and the chosen implementation route. | Pass if the plan names specific file(s) or location(s) to change and commits to one approach, such that someone who has not seen the issue could open those files and start. Fail if a real decision is deferred to build time ("somewhere," "upstream or vendored, whichever is easier," "investigate X, Y, or Z"), or no file/location is named. | required |
| test-plan-decisive | The plan's test plan, read against the repro evidence's steps and artifacts. | Pass if the test plan re-runs a specific step (or a clearly equivalent step) from the repro evidence and states the specific observable outcome that confirms the fix (an exit code, a rendered value, a timing figure, a named behavior at a named step). Fail if the test plan names only a subjective feeling ("should feel fast," "nothing else should feel broken") or a generic action with no stated expected outcome ("run the full test suite"). | required |
| honest-about-unknowns | Claims made in the plan and comment, read against what the repro evidence actually establishes; any stated risks/open questions; any filled `## Deviations` section. | Pass if every claim the plan asserts as fact is supported by the repro evidence or the thread, and anything not yet verified (performance cost, an untested platform, an alternate PR landing first) is explicitly flagged as open rather than asserted as settled. A filled `## Deviations` section (including "nothing changed") stating what changed and why also passes; an unfilled `## Deviations` heading before a build is not itself a fail. Fail if the plan or comment states something as settled fact that the repro evidence does not establish or that a control run contradicts, or if `## Deviations` is filled in a way that contradicts the actual diff. | required |
| comms-thread-aware | The plan comment, read against the thread highlights (or live thread) and the repo-facts block's contribution policy and AI-use disclosure requirement. | Pass if the comment's approach does not ignore or contradict explicit direction already given by a maintainer/owner in the thread (a named culprit, a rejected approach, a requested test, a linked competing PR), AND, when the repo-facts block states an AI-use disclosure requirement, the comment discloses AI assistance. Fail if the approach conflicts with or never engages maintainer direction visibly present in the thread, or omits AI disclosure that the repo's stated policy requires. | required |

## Verdict rule

Accept (ready) only if every required check above grades `pass`. If any
required check grades `fail`, the verdict is `reject`. There are no
`preferred` checks in this rubric; all six are required because each
one maps to a distinct way a plan gets posted and later falls apart
(wrong cause, scope creep, nothing a stranger could start from, a test
that proves nothing, false confidence, or a comment that ignores the
room it's posted into).

`unclear` is treated as `fail` for every check: a plan package that
does not give enough evidence to decide a check is not evidence that
the check is fine, and reject is the safe default when the package
cannot show its work.
