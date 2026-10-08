# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

oimahawong

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6051546700

Hi, I'd like to work on this README/.env.example mismatch as my Unit 2 reproduction. I'll compare the Quick Start instructions in README.md, the complete .env.example template, and the Settings fields in core/config.py against each other — and check docs/SETUP.md too, since it also references the LLM provider setup — to confirm exactly where the OpenRouter key and LLM_PROVIDER guidance disagree. I'll follow up with my own reproduction report recording the commit, environment, and steps I used.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6051806656

Environment: macOS Darwin 27.0.0 (arm64), Python 3.12.4. Fork oimahawong/pathreview-ai301-fa26-s1, commit f89c06f, branch main, clean working tree. Static file inspection only — no app boot, Docker, or API key needed.

$ sed -n '24,25p' README.md
# Configure environment (add your OPENROUTER_API_KEY to .env)
cp .env.example .env

$ cat .env.example # LLM section, complete
# Options: "mock" (default, no API key needed), "openai"
LLM_PROVIDER=mock
OPENAI_API_KEY=sk-your-key-here

No OPENROUTER_API_KEY anywhere in the file.

$ grep -n "openrouter_api_key" core/config.py
20: openrouter_api_key: str = Field(default="")

The field exists in the app's own settings, so this isn't a stale/removed option.

$ grep -n "OPENROUTER" docs/SETUP.md
47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)

A second doc repeats the same instruction.

$ cp .env.example .env && grep -n "OPENROUTER" .env || echo "(no match)"
(no match)

Expected: .env.example contains (or the docs explain how to add) OPENROUTER_API_KEY, consistent with the fields core/config.py defines.

Actual: no OPENROUTER_API_KEY in the template; only mock/openai listed.

Scope: file inspection plus the documented copy step only — did not start the app or test the openrouter provider at runtime.

## Eval iterations

**Run history**

1. First full run: 19/20 scored items agreed with gold (bar: 18/20 — PASS). The one miss was `pkg-05` (gold `accept`, graded `reject`, failing the `Steps-followable` check).
2. Revised `Steps-followable`'s pass condition, then re-ran with `--only pkg-05,pkg-08,pkg-18,pkg-20` (pkg-05 to confirm the fix, plus three canaries: pkg-08 for `wrong-target`, pkg-18 for `unfollowable-comms`, pkg-20 for the single-package `disclosure` category, since a loosened check can flip a package that previously agreed). Result: 4/4 agreed, including pkg-05 flipping to `accept`.
3. Confirming full run, saved with `--save-run eval-run.txt`: **20/20 scored items agreed with gold (bar: 18/20 — PASS)**, category floor met in every category (clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4). This is the run committed in `eval-run.txt`.

**Package analysis**

`pkg-05` (conda/conda#16543, category `clear-accept`, gold verdict `accept`). My rubric's first pass graded it `reject`, failing `Steps-followable`. The candidate repro report describes its triggering input file in prose — "a minimal `env.yml` containing a valid `dependencies:` list plus a `category:` section (the section conda does not recognize)" — rather than pasting the literal YAML. My original check wording required that "every command, input file, and triggering condition... is given in the report itself," which a literal read treats as requiring the raw file content, so the grader failed it for not showing the file verbatim. But the report does pin down the one thing that actually matters: the exact field name (`category:`) that conda's schema rejects, which is enough for a stranger to reconstruct an equivalent file and trigger the same `EnvironmentSectionNotValid` behavior. The gold label calls this a clear accept precisely because the repro is faithful and followable even though it's terse. My rubric was reading the check's own write-up shape (verbatim file dump) instead of the outcome (can someone else recreate the trigger), which is exactly the failure mode `rubric.md`'s own template warns against.

**Check rationale**

The `Steps-followable` check in `rubric.md` as it reads now:

> Pass if a stranger with the stated environment could re-run the same steps and land in the same state: every command and triggering condition the issue requires is given in the report itself (not referenced as living in a private repo, an unshared config, or "my setup"), and any input file's content is either shown verbatim or described precisely enough that the specific triggering element (the exact flag, field, or value that causes the bug) is fully pinned down, even if incidental details are paraphrased. Fail if the trigger depends on a resource the report does not share, if the steps skip the specific condition the issue says causes the bug (e.g. running a plain case instead of the boundary/edge case named in the issue), or if an input file is described too vaguely to pin down the triggering content.

It reads this way because the original version only said an input file must be "given in the report itself," which I'd written with verbatim file contents in mind. `pkg-05` showed that was too strict: a precise prose description of a trivial file can be exactly as followable as pasting it, so I added the clause allowing either form, gated on whether the specific triggering element is pinned down rather than cosmetic completeness. I rejected the alternative of just deleting the input-file requirement entirely, because `pkg-18` (private monorepo, unshared config) needs this same check to still fail on an unfollowable resource — the fix had to loosen "how precisely" without loosening "must be shareable at all."

**Trade-offs**

Loosening `Steps-followable` to accept a precise description in place of a verbatim file trades a small risk: a confidently-written but inaccurate description of an input file could now pass this check even if the actual file (if shown) would reveal a subtly different trigger than described. I accept that risk because the alternative — requiring verbatim file contents always — would keep failing faithful, minimal reports like `pkg-05` on formatting grounds rather than substance, which is the opposite of what the check is supposed to judge. I re-ran canaries after the change (`pkg-08` wrong-target, `pkg-18` unfollowable-comms, `pkg-20` disclosure) specifically because this check also gates those categories, and confirmed none flipped: `pkg-18`'s failure still comes from the trigger living in an unshared private repo (a condition the loosened wording explicitly still fails), and `pkg-08`/`pkg-20` don't depend on this check's wording at all, so they were unaffected either way.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
