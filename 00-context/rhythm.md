# Research rhythm

> *What this file is: the default cadence for synthesis passes, living-artifact
> regeneration, and readouts. Without a default, this work only happens when
> something forces it (usually a deadline), which is too late.*
>
> A default isn't a contract. Trade it deliberately when the situation warrants.

**Last updated:** *(date)*

---

## Why a rhythm

A discovery project has two clocks. The fast clock is per-session: each interview gets a synthesis and the insights file gets updated. That's the per-session workflow already captured in the README.

The slow clock is the *step-back* clock: when do you stop adding sessions and look at the whole? Without a rhythm, the slow-clock work either gets postponed indefinitely (and the insights silently drift from evidence) or it happens in a panicked rush before a stakeholder review (when there's no time to do it well).

---

## Default cadence

| Trigger | What to do | Why |
|---|---|---|
| After every session | Stage 1 per-session workflow (synthesis + insight reconcile + glossary + sample-coverage + consent log) — `/intake` then `/synthesise` | The atomic loop. Doesn't compound if skipped. |
| Any time a `*-review-*.md` is recorded | Re-invoke `/synthesise` for the affected artifact (second-pass behaviour) | Reviews stay raw evidence; reconciliation runs through the same skill |
| After every 3 sessions | Light step-back: `/curate` to regenerate `themes.md` and `INDEX.md`. Refresh `probes.md`. Re-check sample-coverage and decide who to recruit next. | Enough new evidence to see new clusters; not so much that you lose the thread. |
| After every 6 sessions | Full regenerate: `journey-map.md`, `story-map.md`, `stakeholder-map.md`, `personas.md`. Promote `hunch` insights that have earned `emerging` status. | The living artifacts are only trustworthy if rebuilt at this cadence. |
| After every 3–4 sessions, or after a session that felt off | `/coach` pass — review interviewing technique and discovery questions | The method itself needs disconfirmation too. |
| After every 8–10 sessions | Draft or refresh `opportunities.md` from the strongest insights. Write a readout for the stakeholder. | At this point the evidence base is mature enough to start framing openings without overreaching. |
| Whenever an insight is contradicted | Mark `contested`. Don't rewrite. Add to `probes.md`. Consider whether to split the claim. | Contradiction is the most valuable signal. Make sure it's visible. |
| Whenever a decision is made | Append to `03-decisions/decisions-log.md`, with evidence citation. | The chain stays traceable. |
| Whenever the recruitment funnel narrows | Update `00-context/recruitment.md` and consider which gaps in `sample-coverage.md` are now critical. | Otherwise the sample gets defined by who was easy to find. |

---

## What "regenerate" means

The living artifacts (`journey-map.md`, `story-map.md`, `stakeholder-map.md`, `themes.md`, `personas.md`, `opportunities.md`) are **rebuilt from `insights/` and `sessions/`**, not hand-edited. When the rhythm calls for regeneration:

1. Invoke `/curate` (the Curator role / skill) to rebuild from current evidence.
2. Read what it produced and decide if anything in the *underlying* insights or sessions should be sharpened or split. But make those edits at the source, not in the artifact.
3. Re-regenerate if necessary so the artifact reflects the sharpened evidence.

Every regenerated artifact gets a **"Sources at regeneration"** footer listing the session and insight IDs in scope. If those don't match the current state, the artifact is stale — regenerate before relying on it.

The point: artifacts that disagree with their sources are worse than no artifacts at all.

---

## What gets traded when the rhythm slips

If you have to defer something, defer in this order (safest first):

1. **Defer:** Refreshing `opportunities.md` (you can do it in a single concentrated session later).
2. **Defer:** Regenerating personas (lowest information density for the cost).
3. **Defer:** Regenerating story-map or journey-map (rebuildable from a strong insights base).
4. **Don't defer:** Per-session synthesis. If you skip this, the raw transcript will be harder to digest each time you put it off, and insights will go uncaptured.
5. **Don't defer:** Updating `sample-coverage.md` and `consent-log.md`. These compound the most painfully if neglected.
6. **Don't defer:** Updating `probes.md` when an insight changes status. The whole disconfirmation loop depends on this being current.
7. **Don't defer:** Processing recorded reviews. Reviews are raw evidence; leaving them unreconciled defeats the point of capturing them.
