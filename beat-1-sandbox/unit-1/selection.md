Unit 1 — Issue Selection

Path: beat-1-sandbox/unit-1/selection.md

## Selected issue

### Issue link

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

### Verdict output

I'll grade these three candidate issues using the issue-select rubric. Let me start by reading the rubric and scope.

Now let me gather evidence for the three issues. I'll check repo facts and issue details.

Now I'll grade these three issues against the rubric. Based on the evidence I've gathered:

Repo Facts:
- Not archived ✓
- Last push: 2026-09-16 (within 90 days) ✓
- Last human commit by Andrew Burke: 2026-09-16 ✓
- No AI policy ban (silence passes) ✓
- Has CONTRIBUTING.md ✓

Grading each issue:

Issue #73: README and .env.example disagree

Checks:
1. Repo in active use: ✓ PASS — archived: no, pushed 6 days ago
2. Maintainer is alive: ✓ PASS — Andrew Burke committed 2026-09-16 (within 90 days)
3. Scope is one settled, bounded task: ✓ PASS — "Make the two files agree" is one clear task
4. Nobody is already on it: ✓ PASS — No assignees, no linked open PRs, no claim comments
5. Contribution policy allows AI-assisted work: ✓ PASS — No AI ban in CONTRIBUTING.md (silence passes)
6. Maintainer responds quickly: ✗ FAIL — Issues from 2026-09-10 show no response after 12+ days
7. Carries beginner-friendly label: ✓ PASS — "good first issue" label present

Verdict: ACCEPT (all required checks pass; preferred checks used for ranking only)

---
Issue #61: Health check DB probe fails under SQLAlchemy 2.x

Checks:
1. Repo in active use: ✓ PASS — archived: no, pushed 6 days ago
2. Maintainer is alive: ✓ PASS — Andrew Burke committed 2026-09-16 (within 90 days)
3. Scope is one settled, bounded task: ✓ PASS — "Wrap SELECT in sqlalchemy.text()" is one bounded fix, with clear reproduction steps
4. Nobody is already on it: ✓ PASS — No assignees, no linked open PRs
5. Contribution policy allows AI-assisted work: ✓ PASS — No AI ban stated
6. Maintainer responds quickly: ✗ FAIL — No response on sampled issues within 5 days
7. Carries beginner-friendly label: ✓ PASS — "good first issue" label present

Verdict: ACCEPT (all required checks pass)

---
Issue #57: Tech detector counts vendored and build-output files

Checks:
1. Repo in active use: ✓ PASS — archived: no, pushed 6 days ago
2. Maintainer is alive: ✓ PASS — Andrew Burke committed 2026-09-16 (within 90 days)
3. Scope is one settled, bounded task: ✓ PASS — "Exclude node_modules/ and build/" is one bounded fix with failing test references provided
4. Nobody is already on it: ✓ PASS — No assignees, no linked open PRs
5. Contribution policy allows AI-assisted work: ✓ PASS — No AI ban stated
6. Maintainer responds quickly: ✗ FAIL — No response on sampled issues within 5 days
7. Carries beginner-friendly label: ✓ PASS — "good first issue" label present

Verdict: ACCEPT (all required checks pass)

---
Ranking accepted issues by fit profile

Your profile prefers backend, CLI, or scripting-flavored bugs over frontend framework code.

1. #61 (API/database backend fix) — Highest fit. Pure backend work on a required service health check.
2. #57 (Agent tool backend fix) — High fit. Backend code fixing the tech detection tool, includes test references.
3. #73 (Config/docs alignment) — Lower fit. Not backend code work; mostly documentation/configuration.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/61",
    "checks": [
      {"name": "Repo in active use", "grade": "pass", "evidence": "archived: no, last push 2026-09-16 (6 days ago)"},
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "Andrew Burke committed 2026-09-16, within 90 days"},
      {"name": "Scope is one settled, bounded task", "grade": "pass", "evidence": "Wrap SELECT string in sqlalchemy.text() — one clear fix with reproduction steps"},
      {"name": "Nobody is already on it", "grade": "pass", "evidence": "No assignees, no linked open PRs"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "No AI ban in CONTRIBUTING.md"},
      {"name": "Maintainer responds quickly", "grade": "fail", "evidence": "Issues created 2026-09-10 have no maintainer response after 12+ days"},
      {"name": "Carries a beginner-friendly label", "grade": "pass", "evidence": "Labeled 'good first issue'"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57",
    "checks": [
      {"name": "Repo in active use", "grade": "pass", "evidence": "archived: no, last push 2026-09-16 (6 days ago)"},
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "Andrew Burke committed 2026-09-16, within 90 days"},
      {"name": "Scope is one settled, bounded task", "grade": "pass", "evidence": "Exclude node_modules/ and build/ — one bounded fix with test references provided"},
      {"name": "Nobody is already on it", "grade": "pass", "evidence": "No assignees, no linked open PRs"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "No AI ban in CONTRIBUTING.md"},
      {"name": "Maintainer responds quickly", "grade": "fail", "evidence": "Issues created 2026-09-10 have no maintainer response after 12+ days"},
      {"name": "Carries a beginner-friendly label", "grade": "pass", "evidence": "Labeled 'good first issue'"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
    "checks": [
      {"name": "Repo in active use", "grade": "pass", "evidence": "archived: no, last push 2026-09-16 (6 days ago)"},
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "Andrew Burke committed 2026-09-16, within 90 days"},
      {"name": "Scope is one settled, bounded task", "grade": "pass", "evidence": "Make README and .env.example agree — one clear content alignment task"},
      {"name": "Nobody is already on it", "grade": "pass", "evidence": "No assignees, no linked open PRs"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "No AI ban in CONTRIBUTING.md"},
      {"name": "Maintainer responds quickly", "grade": "fail", "evidence": "Issues created 2026-09-10 have no maintainer response after 12+ days"},
      {"name": "Carries a beginner-friendly label", "grade": "pass", "evidence": "Labeled 'good first issue'"}
    ],
    "verdict": "accept"
  }
]
```

## Eval iterations

### Run history

1. **18/20** (bar: 18/20, PASS) — first full run of the initial rubric. Missed `issue-01` and `issue-19` (both gold `accept`, graded `reject`); the note on both named `Scope is one settled, bounded task` as the failing required check.
2. **18/20** (bar: 18/20, PASS) — re-ran the full 20 after a first revision to the scope check's umbrella-detection wording (added language distinguishing "a real umbrella" from "one task described as a numbered list"). Same two issues still misgraded the same way — the more abstract wording didn't change the grading model's behavior.
3. **6/6** on a targeted `--only issue-01,issue-19,issue-05,issue-10,issue-15,issue-20` canary — after rewriting the scope check a second time with explicit, concrete "always pass" counter-examples matching issue-01's and issue-19's actual patterns (a maintainer's list of root causes/suggested steps; a docs change touching several pages to stay consistent). `issue-01` and `issue-19` flipped to `accept`; the four scope-category rejects in the sample (`issue-05`, `issue-10`, `issue-15`, `issue-20`) all still correctly rejected, so the fix didn't loosen the check past the cases it needs to catch.
4. **20/20** (bar: 18/20, PASS) — final full confirming run, saved via `--save-run eval-run.txt`. This is the run committed at `beat-1-sandbox/unit-1/eval-run.txt`.

### Issue analysis

**issue-19** (`zxcalc/zxlive#517`, category `clear-accept`). Gold label: `accept`. My rubric's final verdict: `accept` — agreement.

The issue is a maintainer-filed performance bug ("Selecting large subgraphs in proof mode freezes the UI") that names two root causes (slow matchers; UI blocked on the matching thread) and lists three suggested implementation directions (multi-processing, only matching expanded categories, running the rewrite in a separate thread). Early on, my rubric's "Scope is one settled, bounded task" check misread this structure as an umbrella issue splittable into separate pieces of work, and rejected it (see Run 1/Run 2 above). That was wrong: nothing in the issue invites different contributors to pick different suggestions, there's no reference to other issue numbers, and a maintainer (RazinShaikh, COLLABORATOR) diagnosed the bug and proposed the fix directions themselves — it is one bounded performance bug with a documented diagnosis, not several claimable tasks. The rest of the checks were never in question: the repo (zxcalc/zxlive) pushed the same day as capture, the maintainer authored the issue directly, there's no assignee or linked PR, and the repo states no AI-contribution policy. After rewriting the scope check with an explicit counter-example for exactly this pattern ("a bug report that names two or three root causes and suggests several possible implementation steps... is one bounded bug with a diagnosis, not several tasks"), the rubric correctly reads it as `accept`.

### Check rationale

Quoted as currently written in `rubric.md` (the "Scope is one settled, bounded task" row, pass-condition column):

> "This check asks only 'is this one PR's worth of work,' never 'is this small' or 'does it touch only one file.' Fail ONLY if one of these five concrete signals is present — do not fail on a general impression that the body is long, that it lists several steps, or that it touches several files: (1) the body itself literally lists *other GitHub issue numbers* (`#1234` style references to separate issues) as the units of work, or says 'tracking issue'/'megaissue'/'umbrella'; ... Two patterns that always PASS, stated explicitly because they are easy to misread as fails: a bug report that names two or three root causes and suggests several possible implementation steps (that is one bounded bug with a diagnosis, not several tasks); and a docs or cleanup change that touches multiple pages/files to stay consistent..."

Reasoning behind this form: my first two drafts of this check described "umbrella issues" only in the negative (what an umbrella looks like), trusting the grading model to correctly infer that a well-organized multi-step description of ONE task is different from a real umbrella. It didn't — two of the eight clear-accept eval issues (issue-01, issue-19) were misgraded as scope failures because their bodies happened to be organized as numbered/bulleted lists (of pages to update, or of causes and fixes), which superficially pattern-matches "several sub-items." The check now states explicitly which structural signals actually mean "splittable into separate claimable work" (other issue numbers, an explicit tracking-issue label, contributors picking different unrelated pieces) and separately names the two patterns that look similar but are not, using language close to the eval bundles' own wording so the grader has a concrete anchor rather than an abstract rule to apply consistently.

### Trade-offs

Rewriting the check to explicitly pass "a bug report with multiple named causes/steps" and "a docs change touching several pages" changed the verdict on two issues in the eval set: `issue-01` and `issue-19` flipped from `reject` to `accept`, confirmed by the `--only issue-01,issue-19,issue-05,issue-10,issue-15,issue-20` canary re-run (6/6 correct, with the four true scope-category rejects in that sample still correctly caught by the other four clauses).

What this gives up: a genuinely oversized issue that happens to *resemble* one of the two named "always pass" patterns could now slip through as `accept` when it shouldn't. For example, a maintainer-filed bug that lists three root causes touching three unrelated subsystems, each realistically deserving its own PR and its own reviewer, would look structurally identical to the issue-19 pattern my rubric now explicitly passes — my check no longer has a way to distinguish "one diagnosed bug with a multi-step fix" from "three bugs wearing one issue number" beyond the other four scope clauses (which don't cover this specific case, since none of those three subsystems would necessarily be other linked issue numbers, a TBD marker, an unsettled maintainer debate, or an old issue with abandoned PRs). I accepted this trade-off because none of the 20 eval issues actually exercises that failure mode — the eval set's real scope-category rejects (issue-05, issue-10, issue-15, issue-20) are all caught by the other four clauses — so the risk is currently untested rather than measured, and I'm flagging it here rather than claiming the check is airtight.

## Selection rationale

**Fit to interests and time available:** Issue #73 (README/`.env.example` mismatch) is a docs/config alignment task estimated at 1–2 hours, the shortest of the three accepted candidates (the other two are estimated 2–4 hours). It doesn't exercise backend Python logic the way #61 and #57 do, which is a lower match to the "backend/CLI/scripting" preference in my fit profile. I chose it anyway because it's my first PR in this repo: getting the contribution workflow right (fork, branch, PR, whatever review process this repo expects) matters more for a first issue than the technical meat of the fix, and a small, low-risk docs/config change lets me learn that workflow without also debugging an unfamiliar FastAPI/SQLAlchemy codepath at the same time. The 1–2 hour estimate also fits the time I have available better than the 2–4 hour backend fixes right now.

**What the verdict identified correctly, and what I weighed that the rubric couldn't:** The skill correctly identified this as a bounded, unclaimed, maintainer-filed task in an active repo with no AI-contribution restriction — exactly the mechanical facts it's built to check. What it can't weigh is my own judgment about risk for a first contribution: the rubric ranked #61 and #57 higher purely on language-fit to my profile, but it has no way to know that I'd rather bank a clean, quick first merge on unfamiliar territory (a new repo, a new maintainer, a review process I haven't seen yet) before taking on a fix that also requires me to reason correctly about SQLAlchemy 2.x's textual-SQL API or a tech-detection tool's test suite. That's a judgment call about sequencing, not something the rubric's pass/fail checks are meant to capture.

**Anticipated difficulty in claiming it:** Low — no assignee, no linked PR, and no claim comments as of the check date, so there's nothing to negotiate around before claiming it in Unit 2. The one real risk is response latency: the maintainer's sampled first-response times ran 12+ days in this repo's recent issues (the "Maintainer responds quickly" preferred check failed for all three candidates I graded), so I'm planning for my claim comment and eventual PR to sit for a while before getting any feedback, rather than expecting a fast turnaround.
