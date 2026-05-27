# Research cadence

> [!NOTE]
> **What this file is.** The default cadence for synthesis passes, living-artifact regeneration, and readouts. Without a default, this work only happens when something forces it (usually a deadline), which is too late.

> [!TIP]
> A default isn't a contract. Trade it deliberately when the situation warrants.

- **Last updated:** *YYYY-MM-DD.*

---

## Why a cadence

A discovery project runs on two clocks.

**The fast clock is per-session.** Each interview gets a synthesis and the insights are updated. That's the atomic loop already captured in the README.

**The slow clock is step-back.** When do you stop adding sessions and look at the whole? Without a cadence, the slow-clock work either gets postponed indefinitely (and insights silently drift from evidence) or it happens in a panicked rush before a stakeholder review — when there's no time to do it well.

---

## Default cadence

| Trigger | What to do | Why |
| --- | --- | --- |
| After every session | Per-session workflow: `/intake` then `/synthesise`. Updates synthesis, insights, glossary, sample-coverage, consent-log. | The atomic loop. Compounds if skipped. |
| Any time a `*-review-*.md` is recorded | Re-invoke `/synthesise` for the affected artifact. | Reviews stay raw evidence. Reconciliation runs through the same skill. |
| After every 3 sessions | Light step-back: `/curate` to regenerate `02-synthesis/themes.md` and `02-synthesis/insights/INDEX.md`. Refresh `02-synthesis/probes.md`. Re-check sample coverage and decide who to recruit next. | Enough new evidence to see new clusters; not so much that you lose the thread. |
| After every 6 sessions | Full regenerate: `02-synthesis/journey-map.md`, `02-synthesis/story-map.md`, `02-synthesis/stakeholder-map.md`, `02-synthesis/personas.md`. Promote `hunch` insights that have earned `emerging`. | The living artifacts are only trustworthy if rebuilt at this cadence. |
| After every 3–4 sessions, or after a session that felt off | `/coach` pass. Review interviewing technique and discovery questions. | The method itself needs disconfirmation too. |
| After every 8–10 sessions | Draft or refresh `02-synthesis/opportunities.md` from the strongest insights. Write a readout for the stakeholder. | The evidence base is mature enough to frame openings without overreaching. |
| Whenever an insight is contradicted | Mark `contested`. Don't rewrite. Add to `02-synthesis/probes.md`. Consider whether to split the claim. | Contradiction is the most valuable signal. Make sure it stays visible. |
| Whenever a decision is made | Append to `03-decisions/decisions-log.md`, with evidence citation. | The chain stays traceable. |
| Whenever the recruitment funnel narrows | Update `01-research/method/recruitment.md` and check which gaps in `01-research/method/sample-coverage.md` are now critical. | Otherwise the sample gets defined by who was easy to find. |

---

## What "regenerate" means

The living artifacts in `02-synthesis/` (`journey-map`, `story-map`, `stakeholder-map`, `themes`, `personas`, `opportunities`) are **rebuilt from `02-synthesis/insights/` and `01-research/sessions/`**, not hand-edited.

When the cadence calls for regeneration:

1. Invoke `/curate` to rebuild from current evidence.
2. Read what it produced. If the *underlying* insights or sessions need sharpening or splitting, make those edits at the source.
3. Re-regenerate so the artifact reflects the sharpened evidence.

> [!IMPORTANT]
> Every regenerated artifact carries a **Sources at regeneration** footer listing the session and insight IDs in scope. If those don't match the current state, the artifact is stale — regenerate before relying on it.

Artifacts that disagree with their sources are worse than no artifacts at all.

---

## What gets traded when the cadence slips

If you have to defer something, defer in this order — safest first.

**Safe to defer:**

1. Refreshing `02-synthesis/opportunities.md`. You can rebuild it in a single concentrated session later.
2. Regenerating personas. Lowest information density for the cost.
3. Regenerating story-map or journey-map. Rebuildable from a strong insights base.

> [!WARNING]
> **Don't defer these. They compound painfully.**
>
> - Per-session synthesis. The raw transcript gets harder to digest each time you put it off, and insights go uncaptured.
> - Updating `01-research/method/sample-coverage.md` and `01-research/method/consent-log.md`. Both compound the most.
> - Updating `02-synthesis/probes.md` when an insight changes status. The disconfirmation loop depends on this being current.
> - Processing recorded reviews. Reviews are raw evidence; leaving them unreconciled defeats the point of capturing them.
