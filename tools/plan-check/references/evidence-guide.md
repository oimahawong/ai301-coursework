# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: in an eval bundle, the candidate plan's opening
"Diagnosis"/"Cause" line(s), read against every numbered step, artifact
(stack trace, timing output, log excerpt), and control run in the
`## Repro evidence` block. In live mode, the plan's diagnosis section
read against the student's own posted repro comment on the issue (or,
on the house issue, the house repro pack), and against anything the
issue body or thread itself already pins down.

What good looks like: the stated cause accounts for every step in the
repro evidence, including control runs. A control run that isolates
one variable ("same steps with X disabled: passes," "same steps on
Linux: works") is the strongest signal — a diagnosis that the control
rules out is wrong even if it sounds confident and well-written. A
diagnosis that simply restates the issue reporter's guess without
checking it against the repro evidence's own controls is unverified,
not grounded.

## Scope

Where it lives: the plan's explicit in-scope/not-in-scope statement
(or an equivalent "Change:"/"Approach:" section with a stated
deferral), read against the symptom the issue and repro evidence
describe — not against what else might be nice to fix nearby.

What good looks like: one bounded change that a maintainer could review
in isolation. A not-in-scope line that names what is deliberately
deferred (and ideally why) is a strong positive signal, especially when
it defers a bigger rework the thread itself raised (see pkg-09-style
plans: "option 2 now, option 1 is a bigger rework, deferred"). A drive-by
rewrite, a new config option nobody asked for, a module restructure, a
dependency migration, or "while I'm in there, I'll also..." are the
tell — even when the core one-line fix embedded inside them is correct,
the package fails this check, because a stranger reviewing the PR
cannot separate the asked-for fix from the unasked-for rework.

## Executability

Where it lives: the plan's approach/steps section — specifically
whether it names file paths, functions, or modules, and whether it
commits to one implementation route.

What good looks like: a named file or location (`src/walk.rs`, "the
push completion callback in `sync_controller.go`") and a single chosen
approach. "Profile it and see," "recover() somewhere," "investigate
whether X or Y," "whichever is easier" are deferred decisions, not
plans — a stranger reading them cannot open an editor and start. A plan
can still name real unknowns (see Honesty below) and remain
executable, as long as the executable part — what gets touched first —
is concrete.

## Test plan

Where it lives: the plan's test plan section, read against the
specific steps and artifacts named in `## Repro evidence`.

What good looks like: the test plan re-runs a named repro step (or an
equivalent through the real code path) and states what observable
result would mean the fix worked — an exit code, a specific rendered
color/value, a timing number in the same units the repro used, a named
behavior at a named step ("step 3 must show the pushed color without
leaving the view"). "Should feel fast," "nothing else should feel
broken," or "run the full test suite" with no named expected outcome
for the fix itself are not decisive, however reasonable they sound —
they give a reviewer nothing to check against.

## Honesty

Where it lives: the plan's stated risks/unknowns/open questions, read
against claims made elsewhere in the same plan and comment; and, when
present, a filled `## Deviations` section at the end of `plan.md`.

What good looks like: a plan that tells apart what the repro evidence
proved from what it hasn't checked yet — "I have not yet measured the
per-print cost of this; if it shows up in the benchmark I'll move the
check," or "deferring the Windows variant, which I can't test here" —
and says so plainly rather than asserting it as settled. This is a
positive signal even in an otherwise terse plan; honest hedging is not
the same as vagueness (compare to Executability: a real unknown stated
plainly next to a concrete chosen first step is fine; a whole approach
left as an unknown is not). A `## Deviations` section is graded only
once it has content: before a build it is expected to be an empty
heading, and that alone is not a fail; after a build, "nothing
changed" in the student's own words is as valid as a detailed account,
but an entry that contradicts what the actual diff did is not.

## Comms

Where it lives: the candidate plan comment, read against two things —
the `## Thread highlights` block (or the live thread) for maintainer
direction already given, and the `## Repo facts` block's stated
contribution policy and AI-use disclosure requirement.

What good looks like: the comment visibly engages whatever a
maintainer/owner already said in the thread — naming the same culprit
file/line they pointed at, adopting (or explicitly and respectfully
declining) an approach they proposed, answering a question they asked
— rather than proposing something that quietly conflicts with or never
acknowledges it (a docs-only workaround posted after the owner already
found the code-level culprit and asked for testing is the textbook
miss). Separately, when `## Repo facts` states an AI-use disclosure
requirement, the comment must disclose AI assistance in some form,
regardless of how good the plan underneath it is — a comment can get
every other check right and still fail here by omitting a
required disclosure line.
