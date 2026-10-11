# Plan: issue #73 — README and `.env.example` disagree about which LLM API key to set

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

## Diagnosis

Building on my Unit 2 repro comment (posted 2026-10-08, quoted in full below),
the three places that describe LLM configuration do not actually disagree on
whether OpenRouter is supported — they agree it is. The gap is narrower than
"the docs disagree": it's that one specific file never got updated to match.

From my repro:

> `$ sed -n '24,25p' README.md`
> `# Configure environment (add your OPENROUTER_API_KEY to .env)`
> `cp .env.example .env`
>
> `$ grep -n "OPENROUTER" docs/SETUP.md`
> `47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)`
>
> `$ grep -n "openrouter_api_key" core/config.py`
> `20:    openrouter_api_key: str = Field(default="")`
>
> The field exists in the app's own settings, so this isn't a stale/removed
> option. ... No OPENROUTER_API_KEY anywhere in the file [`.env.example`].

So: two docs (`README.md`, `docs/SETUP.md`) and the app's own settings class
all name `OPENROUTER_API_KEY`, while `.env.example` — the template a new
contributor actually runs `cp` on per the README's own Quick Start step —
only defines `LLM_PROVIDER` (`mock`/`openai`) and `OPENAI_API_KEY`. A
contributor who follows the README literally ends up with a `.env` that has
nowhere to put the key the README just told them to set.

Establishing that mismatch is as far as my repro evidence goes. It does not
settle *which side* should change: extending `.env.example` to match the two
docs and the config class, versus retargeting `README.md`/`docs/SETUP.md`
toward `openai` instead, are both ways to make the files agree, and my repro
comment's own Expected line left that open ("the template should include
that variable **or** clearly explain how to add it"). I'm treating this as a
genuinely open question (see Risks), not a settled fact, and the scope below
explains why I'm choosing the `.env.example` side anyway.

I independently re-verified, beyond what my repro comment covered, whether
anything in the codebase actually reads `llm_provider` to branch on its
value (relevant because it bears on whether the `# Options:` comment line
needs to change too):

```
$ grep -rn "llm_provider\|openrouter_api_key\|OPENROUTER" --include="*.py" .
core/config.py:18:    llm_provider: str = Field(default="mock")
core/config.py:20:    openrouter_api_key: str = Field(default="")
```

No other module reads either field. `llm_provider` and `openrouter_api_key`
are both declared but currently inert outside `core/config.py` itself. This
matters for scope below.

## Scope

**In:** `.env.example` only — add an `OPENROUTER_API_KEY` placeholder line to
the `# LLM provider` block, directly under `OPENAI_API_KEY`, matching the
file's existing placeholder style (`sk-...-key-here`).

**Not in:**
- `README.md` / `docs/SETUP.md` — both already name `OPENROUTER_API_KEY`,
  consistent with extending `.env.example` to match them. I'm not proposing
  changes to either in this plan; if a maintainer prefers the other
  direction (retargeting the docs toward `openai` instead), that's a
  different, larger change than this one.
- `core/config.py` — the field and default already exist; no behavior change.
- The `# Options: "mock" (default, no API key needed), "openai"` comment line
  — adding `"openrouter"` there would claim the app can select that provider
  at runtime, which my grep above shows is not true yet (no code branches on
  `llm_provider`). Documenting an option that does nothing would just create
  a second, different documentation mismatch. Leaving this line alone is a
  deliberate choice, not an oversight.
- Any change to which provider is actually used at runtime, or to
  `OPENROUTER_BASE_URL` / `OPENROUTER_MODEL`'s existing defaults.

This keeps the fix to exactly what the issue asks ("make the two files
agree") without quietly expanding into provider-selection behavior the issue
never raised and my reproduction never tested.

## Files I'll touch

- `.env.example` (one addition: one new line, under the existing
  `OPENAI_API_KEY` line in the `# LLM provider` block)

## Approach

1. On branch `fix/73-openrouter-env-example`, open `.env.example`.
2. Directly under the existing `OPENAI_API_KEY=sk-your-key-here` line, add:
   ```
   OPENROUTER_API_KEY=sk-or-your-key-here
   ```
3. Leave the `# Options:` comment line, `LLM_PROVIDER=mock` default, and
   every other line untouched.
4. Confirm with `git diff` that `.env.example` is the only file touched and
   the diff is purely additive.

## Test plan

Re-running my Unit 2 repro steps against the change:

- Before (from my repro comment): `cp .env.example .env && grep -n "OPENROUTER" .env` → `(no match)`.
- After: the same command must print a line matching `OPENROUTER_API_KEY=`.
- Before/after, unchanged: `grep -n "OPENAI_API_KEY" .env.example` still
  matches exactly once, and `LLM_PROVIDER=mock` is still the default — i.e.
  the existing OpenAI path and default behavior are provably untouched by
  this diff, not just assumed to be.
- `git diff --stat` after the change must show exactly one file
  (`.env.example`) with only additions, confirming the scope line above held.

## Risks and unknowns

- I have not established whether a maintainer actually wants `.env.example`
  extended (this plan's direction) versus the docs retargeted toward
  `openai` instead (the other direction the issue's "make the two files
  agree" phrasing leaves open). My repro evidence favors extending
  `.env.example`, since two independent docs and the config class already
  commit to `OPENROUTER_API_KEY`, and retargeting both docs would be the
  larger change for no stated reason. I'm flagging this as a real unknown
  rather than asserting it's settled.
- Several other students have posted plans on this same issue proposing the
  same narrow `.env.example` addition. I checked PR #77 (linked on the issue)
  myself rather than relying on others' in-thread description of it: its diff
  touches only `.env.example` (+2/-1) and `README.md` (+2/-1) — no `.py`
  files — so it is docs-only, not runtime support. It goes further than my
  plan in one specific way: it also edits the `# Options:` comment line to
  add `"openrouter"`, and rewords the README's Quick Start comment. Since my
  own check of the codebase (above) found nothing that reads `llm_provider`
  to select a provider, I'm not confident that edit is accurate yet, which is
  part of why my plan leaves that line alone. I am not adopting PR #77's
  approach; this plan is built from my own repro and reasoning above.

## Deviations

Nothing changed. The build matched this plan exactly: one line,
`OPENROUTER_API_KEY=sk-or-your-key-here`, added to `.env.example` directly
under `OPENAI_API_KEY`, on branch `fix/73-openrouter-env-example`
(commit `cd42fe1`). No other file was touched, and `git diff --stat` shows
exactly the one-file, one-insertion change this plan described.
