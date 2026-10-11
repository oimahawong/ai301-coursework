
# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

---

## Posted upstream

**GitHub username**

oimahawong

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6106871629

Reproduced independently (my report above, 2026-10-08): README.md:24-25 and docs/SETUP.md:47 both instruct setting OPENROUTER_API_KEY, and core/config.py:20 declares a matching openrouter_api_key field, so this isn’t a stale reference. .env.example is the one file that doesn’t match: it defines LLM_PROVIDER and OPENAI_API_KEY but never OPENROUTER_API_KEY, so following the README’s own cp .env.example .env step leaves no place to put the key it just asked for. That tells me the three sources disagree; it doesn’t by itself tell me which side should change.

Plan: add one OPENROUTER_API_KEY=sk-or-your-key-here line to .env.example’s LLM provider block, under the existing OPENAI_API_KEY line. I checked whether any code currently branches on llm_provider’s value (grep -rn "llm_provider\|openrouter_api_key" --include="*.py" .) and found only the two declarations in core/config.py — no runtime selection logic exists yet.

Re: PR #77, already linked here — I checked its diff directly rather than go on description alone: it’s docs-only too (.env.example +2/-1, README.md +2/-1, no .py changes), and it goes further than my plan by also adding "openrouter" to the # Options: comment. Given what I found above (nothing reads llm_provider yet), I’m not confident that comment update is accurate, which is why my plan leaves that line alone rather than claim a provider switch exists when I can’t show it does.

Open question I don’t have an answer to: whether .env.example should be the side that changes (my plan and PR #77’s direction) versus retargeting the docs toward openai instead. I’ll hold off opening a PR until that’s clearer, or adjust if review says otherwise.

(AI disclosure: I used Claude to help draft this plan and comment from my own reproduction; I verified the grep results above myself.)

---

## Your branch

**Branch**

fix/73-openrouter-env-example

**Evidence**

Before (main, via `git show main:.env.example`):
```
$ grep -n "OPENROUTER" /tmp/.env.before || echo "(no match)"
(no match)
```

After (this branch, `.env.example` with the fix applied):
```
$ cp .env.example .env
$ grep -n "OPENROUTER" .env || echo "(no match)"
20:OPENROUTER_API_KEY=sk-or-your-key-here
```

Unchanged, confirmed on the same branch:
```
$ grep -n "OPENAI_API_KEY" .env.example
19:OPENAI_API_KEY=sk-your-key-here
$ grep -n "LLM_PROVIDER=mock" .env.example
18:LLM_PROVIDER=mock
```

Diff scope, confirmed against `main`:
```
$ git diff --stat main
 .env.example | 1 +
 1 file changed, 1 insertion(+)
```

## Eval iterations

**Run history**

One full run: `python3 run_eval.py --rubric skill/rubric.md --evidence skill/references/evidence-guide.md --save-run eval-run.txt`, grading the complete rubric/procedure/evidence-guide set — 19/20 agreement (bar: 18/20: PASS), with every composition category matched at least once (clear-accept 6/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4). This run's agreement score (19/20) is the one recorded in the committed `eval-run.txt`. No revisions were made and no partial `--only` reruns were needed, since the bar was already cleared on this first full run.

**Package analysis**

pkg-14 (zellij-org/zellij#5174): gold label is `accept`, my rubric graded `reject` (failed `diagnosis-grounded` and `honest-about-unknowns`). The plan is a genuinely strong, honestly-scoped reattach-handshake fix: it's grounded in a clean version regression (0.44.1 clean, 0.44.2 leaking) and a cache-clear control, bounds itself to the Unix client path, and explicitly defers the untestable Windows variant with a stated reason. My rubric reads it stricter than gold does on two points: the stated mechanism ("stdin wired before query responses are consumed") is inferred from correlation rather than isolated by a direct control the way other accepted packages' diagnoses are, and the plan asserts "I have [debug tracing] working" as settled fact without that tracing appearing anywhere in the package's own repro-evidence block. Gold treats this as defensible under the deferral; my rubric treats the unverified debug-tracing claim and the inferred mechanism as exactly what `honest-about-unknowns` and `diagnosis-grounded` are built to catch. I judged this a legitimate stricter-reading disagreement rather than a rubric bug, so I left the checks as written rather than risk flipping the wrong-cause/clear-accept packages that already agree.

**Check rationale**

Quoted exactly from the uploaded `rubric.md`'s `comms-thread-aware` row, pass condition: "Pass if the comment's approach does not ignore or contradict explicit direction already given by a maintainer/owner in the thread (a named culprit, a rejected approach, a requested test, a linked competing PR), AND, when the repo-facts block states an AI-use disclosure requirement, the comment discloses AI assistance. Fail if the approach conflicts with or never engages maintainer direction visibly present in the thread, or omits AI disclosure that the repo's stated policy requires." It reads as a conjunction of two independent conditions because the eval set's thread-convention category is built from two unrelated failure modes: pkg-04 ignores an owner's already-identified culprit and request for testing, while pkg-20 follows the thread's direction perfectly but omits AI disclosure the repo's policy requires. A check that only tested one half would structurally miss one of the two packages in this category, and the category floor requires at least one match — so the pass condition has to fail on either violation independently, not just their combination. I didn't revise this check after the first run; it read both calibration/practice packages in this category correctly on the first full run.

**Trade-offs**

Combining both conditions into one named check trades away diagnostic specificity: when this check fails, the output's `evidence` field has to carry which half broke (thread-ignoring vs. missing disclosure), but the check's `name` alone doesn't distinguish a plan that nailed the thread but forgot disclosure from one that ignored the maintainer entirely. A rubric with two separate checks (`comms-thread-direction` and `comms-ai-disclosure`) would give a student clearer, separately-actionable feedback on which problem to fix, at the cost of one more row in an already six-row required table. I chose the combined check to keep the check count focused on distinct failure families from the lecture rather than splitting one family into sub-checks, and confirmed nothing changed elsewhere because this check graded both `thread-convention` packages (pkg-04, pkg-20) correctly on the single full run — no `--only` canary rerun was needed since I never loosened or tightened this check after that run.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; skill's files in `tools/plan-check/`.
