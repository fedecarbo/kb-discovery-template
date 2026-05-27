# Review of cpca-kb-discovery (follow-up)

**Reviewer:** Claude (AI workflow engineer + user researcher lens)
**Date:** 2026-05-27
**Scope:** Full repo at HEAD on `main` after the recent restructure. Read-through pass requested by the user after "lots of changes throughout."
**Prior review:** [system-review-2026-05-26.md](system-review-2026-05-26.md) — still substantively right on methodology, partially stale on file paths.

---

## Context

You asked for an honest read after a wave of changes. This is an assessment, not an implementation plan. A small "if you want to act" section is at the end so the next step is yours to pick.

The most concrete signal of what your changes did: you collapsed `00-context/` into truly stable framing only (problem, vision, questions) and pushed everything operational into `01-research/method/`. The renames were `method-notes.md` → `coaching-log.md`, `rhythm.md` → `cadence.md`, plus moves of `consent-log.md`, `glossary.md`, `recruitment.md`, `sample-coverage.md`. That move is right — context is now genuinely stable, method lives next to the data it shapes.

---

## Headline

The design is unusually good, and the recent restructure improved it. The four skills are still mutually consistent after the moves, every path the skills reference still resolves, and the audit-trail discipline (reads / writes / does NOT touch) holds. **What isn't working is mostly that nothing has been run yet** — every file outside the README, syntax-guide, and skill definitions is a template waiting for its first session. Several smaller drift items have appeared, listed below.

---

## What's working

- **The 00-context → 01-research/method split is now coherent.** 00-context is genuinely stable framing; method lives next to the data it shapes. Cross-references inside the skills all resolve to the new locations — no dangling references from the rename.
- **Skill chaining is intact end-to-end.** Intake → Synthesise (first pass) → human review → Synthesise (second pass) → Curate → Coach. Every file one skill writes is one another reads, and the read/write boundaries match the templates.
- **Footer pattern is consistent across most living artifacts.** `themes.md`, `personas.md`, `journey-map.md`, `story-map.md`, `stakeholder-map.md`, `opportunities.md`, `probes.md`, and `insights/INDEX.md` all use the curate-compatible "Sources at regeneration" block with the same stale-detection callout.
- **The disconfirmation-status ladder and chain-of-evidence rule** (the two things the prior review called out as genuinely uncommon) are still in place and load-bearing.
- **syntax-guide.md** is precise and complete — useful as a guardrail when the skills start writing into the artifacts.
- **Templates match what the skills expect to read.** `_TEMPLATE-session/{interview,reflection,guide,synthesis}.md`, `_TEMPLATE-review.md`, `_TEMPLATE-insight.md`, `_TEMPLATE-usability-test.md` are all referenced consistently.

---

## What isn't working

### Blocking-ish

1. **`.claude/settings.local.json` points at the wrong directory.** Lines 4 and 8 reference `/Users/fedecarbo/Downloads/cpca-discovery/.claude/skills`, but the project lives at `/Users/fedecarbo/Documents/cpca-kb-discovery/`. The `additionalDirectories` entry and the pre-baked `mkdir` permission are both pointing at the old location. This will fight you the first time you invoke a skill. Easiest fix: delete the `additionalDirectories` entry entirely (the skills already live inside the repo at `.claude/skills/`, so the extra search path isn't needed) and drop the stale `mkdir` allow-rule.

2. **`02-synthesis/jobs-to-be-done.md` uses a different footer scheme** than every other living artifact. Line 6 has `**Last updated:** *YYYY-MM-DD*` + `**Source sessions:**` instead of the `## Sources at regeneration` block with both Sessions and Insights lists. The Curate skill regenerates this file too, so the footer should match. Without the fix, the staleness sensor won't fire on JTBD, and the curator either has to special-case JTBD or quietly overwrite the header.

### Drift / methodology gaps the prior review already flagged, still unresolved

The 2026-05-26 review calls these out in more detail; the short version:

3. **No worked example.** Every populated file is a template. A `_EXAMPLE-session/` end-to-end (transcript → reflection → synthesis → derived insights → themed probes) would give the skills a concrete reference on first run.
4. **Coach proposals have no status field.** `coaching-log.md` accumulates proposals; nothing distinguishes `proposed` from `applied YYYY-MM-DD` from `rejected (reason)`. After 4–5 Coach runs this becomes unsearchable.
5. **`strong` threshold may be unreachable in practice.** README:126 defines it as needing a participant picked because they were *likely* to contradict. In civic / advisory contexts you often can't pre-select. Loosen to a boundary-case test (one participant from the slice most likely to break the claim) or `strong` will never be reached and the ladder loses signal.
6. **No saturation signal in `cadence.md`.** "After 8–10 sessions" tells you when to regenerate, not when the sample is *sufficient*. A "saturation reached when the last 3 sessions added no new insights and challenged no existing ones" rule would close this.
7. **No contested-resolution playbook.** README says "mark contested, don't rewrite" but doesn't say what happens next. Synthesise/SKILL.md should describe the options: split (different mechanism per slice), qualify (true under condition X), or demote.
8. **No upfront target-sample in `sample-coverage.md`.** It records coverage after the fact but there's no statement of who you intended to talk to and why. Without intent, the matrix can't tell you whether you're under-covered.
9. **Interviewer-bias isn't on Coach's checklist.** If you're an insider, you may lead or shorthand. Coach should explicitly scan transcripts for leading questions, premature solutioning, and insider-shorthand echoed without ownership.

### Minor

10. **`docs/system-review-2026-05-26.md` cites paths that no longer exist** (e.g., `00-context/method-notes.md`, `00-context/rhythm.md`). The review is still useful, but worth a header note that paths shifted, or a one-pass path update.

---

## What's deliberately empty (and should stay that way until you run a session)

These looked like "not working" but are correct in their current state:
- `01-research/sessions/` (only `_TEMPLATE-session/` and `_TEMPLATE-review.md` — by design)
- `02-synthesis/insights/` (only `_TEMPLATE-insight.md` + empty `INDEX.md`)
- All living artifacts in `02-synthesis/` (correctly stubbed with "*(none yet — first regeneration follows the cadence...)*")
- `03-decisions/decisions-log.md` (only the seed entry showing the schema)
- `04-outputs/` (empty `handoffs/` is fine pre-readout)

The whole synthesis layer is blocked behind "run `/intake` on the first session." That's the design.

---

## If you want to act

The cheapest changes that materially improve the system, ordered:

1. Fix `.claude/settings.local.json` (5 min, removes a real foot-gun).
2. Bring `02-synthesis/jobs-to-be-done.md` footer in line with the other artifacts (5 min, keeps the staleness sensor working).
3. Add a status field to the `coaching-log.md` proposal template (10 min, prevents future grief).
4. Add target-sample section to top of `sample-coverage.md` (10 min, makes the matrix useful from day one).
5. Build a `_EXAMPLE-session/` worked end-to-end (longer; biggest payoff for first real run).

Items 5–9 in the "What isn't working" list are worth holding until you've done 2–3 real sessions — you'll have a better sense of which ones actually bite.

---

## Critical files referenced

- [README.md](../README.md)
- [.claude/settings.local.json](../.claude/settings.local.json) — path bug
- [.claude/skills/intake/SKILL.md](../.claude/skills/intake/SKILL.md), [synthesise](../.claude/skills/synthesise/SKILL.md), [curate](../.claude/skills/curate/SKILL.md), [coach](../.claude/skills/coach/SKILL.md)
- [02-synthesis/jobs-to-be-done.md](../02-synthesis/jobs-to-be-done.md) — footer divergence
- [01-research/method/coaching-log.md](../01-research/method/coaching-log.md) — needs status field
- [01-research/method/sample-coverage.md](../01-research/method/sample-coverage.md) — needs target plan
- [01-research/method/cadence.md](../01-research/method/cadence.md) — needs saturation signal
- [docs/system-review-2026-05-26.md](system-review-2026-05-26.md) — stale paths after the rename

## Verification (if any changes get made)

- `find .claude/skills -name SKILL.md -exec grep -l "00-context/method-notes\|00-context/rhythm\|00-context/glossary\|00-context/consent-log\|00-context/recruitment\|00-context/sample-coverage" {} \;` should return nothing.
- Every artifact in `02-synthesis/` (except `_TEMPLATE-insight.md` and `insights/`) should end with the `## Sources at regeneration` block — diff their tails to confirm.
- `grep -r "/Users/fedecarbo/Downloads" .claude/` should return nothing after the settings fix.
