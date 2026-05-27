---
name: synthesise
description: Continue session synthesis and reconcile against existing insights. Use after Intake has run on a session, OR as a second pass when a *-review-*.md file exists alongside any artifact in scope. Adds evidence rows, narrows or spawns insights, updates probe notes for affected insights only. Strictly additive — never rewrites insight claims. The review-reconciliation second pass appends a Review-driven updates section and annotates evidence rows; it never silently overwrites first-pass claims.
---

# Synthesist + Reconciler — write synthesis and update insights

> [!NOTE]
> You are running the **Synthesist + Reconciler** role from `README.md § Working with Claude — the four roles § Role B`. That section is the source of truth — if anything here drifts, defer to the README.

## What this skill does

The reasoning-heavy role. You write the cross-cutting parts of `synthesis.md`, then reconcile the session's evidence against the atomic insight set: adding evidence rows, narrowing claims that gain nuance, spawning new insights when a claim genuinely doesn't fit any existing one, and updating probe notes for *affected* insights only.

This skill operates in two modes:

1. **First pass** — runs after Intake on a fresh session.
2. **Second pass (review reconciliation)** — runs when a `*-review-*.md` file exists alongside any artifact in scope.

> [!IMPORTANT]
> On every invocation, scan for `*-review-*.md` files in the directories of the artifacts you're touching. If any unprocessed review files exist, run the second-pass behaviour for those files in addition to (or instead of) the first pass.

---

## When to use this skill

**First pass:**

- Intake has finished on a session. `synthesis.md` has the metadata and Transcription flags filled in; the rest is empty or template.
- `01-research/method/sample-coverage.md`, `01-research/method/consent-log.md`, and `01-research/method/glossary.md` have already been updated.

**Second pass:**

- A `<artifact-base>-review-<YYYY-MM-DD>.md` file exists sibling to any artifact (session synthesis, insight file, living artifact).
- The headline and action items in that review file describe what to reconcile.

---

## Reads

- The Intake output: `synthesis.md` (metadata + Transcription flags), `interview.md`, `reflection.md`.
- `02-synthesis/insights/INDEX.md` — **read this first** to decide which insight files warrant a deep read for this session.
- Individual `02-synthesis/insights/I-*.md` files the INDEX suggests are in scope.
- `02-synthesis/probes.md`.
- `00-context/discovery-questions.md`.
- Any `*-review-*.md` files alongside artifacts you're touching (scan on every invocation).

---

## Writes — first pass

In the session's `synthesis.md`:

- **What we heard** — observations, each backed by a quote.
- **What the reflection added** — observed context beyond the words.
- **Standout moments** — 2–3 things most worth remembering.
- **How this changes the insights** — for each affected insight: reinforces / contradicts / narrows / new / neutral, with rationale.
- **Effect on probes** — for any probe the session was meant to stress-test.

In `02-synthesis/insights/`:

- **Add a new row** to the Evidence table of each affected insight. Never rewrite an existing row.
- **Update status** — `hunch` → `emerging` → `strong` → `contested` per the README's promotion rules. Source count alone isn't enough; the disconfirmation discipline applies.
- **Spawn a new insight file** if a claim doesn't fit any existing one. Use `02-synthesis/insights/_TEMPLATE-insight.md` as the starting structure.

In `02-synthesis/probes.md`:

- Update status notes for **affected insights only**. Don't trim the whole file — that's Curator's job.

---

## Writes — second pass (review reconciliation)

When a `*-review-*.md` file is present:

In the affected `synthesis.md` (or other artifact body):

- Append a `## Review-driven updates (<YYYY-MM-DD from the review filename>)` section. Inside, summarise each action item from the review and what change you made.

In affected `02-synthesis/insights/I-*.md` files:

- Add or correct evidence rows tagged `via review <YYYY-MM-DD>` in the note column. Never silently overwrite a first-pass row.
- Adjust status notes if the review shifts confidence (e.g. moves toward `contested`).

In `02-synthesis/probes.md`:

- Add a probe-status note reflecting the review's input, with the `via review <YYYY-MM-DD>` annotation.

After processing, leave the review file in place — it stays as audit-trail evidence. Don't delete or rewrite it.

---

## Doesn't touch

- Living artifacts (`themes.md`, `journey-map.md`, `story-map.md`, `stakeholder-map.md`, `personas.md`, `opportunities.md`, `INDEX.md`). Those are Curator's.
- Raw transcripts.
- The review transcript itself.
- Insights the session doesn't bear on — touching them adds noise.

---

## Hard rules

> [!IMPORTANT]
> These are non-negotiable. They protect the audit trail.

- **Additive only on claims.** Never rewrite the existing claim text on an insight. If a session narrows the claim, log it in the Disconfirmation section and in the evidence row's note — not by changing the title or the "The claim" paragraph.
- **Spawn before fold when mechanism differs.** Two phenomena that share a domain but have different mechanisms should be separate insights. Different shapes of the same problem still count as different mechanisms.
- **Status follows disconfirmation, not source count.** `emerging` requires ≥1 probe live going into a session that *could* have contradicted. `strong` requires a deliberate disconfirmation attempt that failed. Two supporting sources alone keep an insight at `hunch`.
- **Sample-bias flags travel with the status.** If two consecutive sessions come through the same channel and support the same cluster of insights, the cluster cannot graduate past `hunch` until a non-channel-routed session lands. Record this in the insight's Status line and in `02-synthesis/probes.md`.
- **Reviews never silently overwrite first-pass claims.** Every change must carry a `via review <YYYY-MM-DD>` annotation so the audit trail survives.

---

## Model recommendation

Sonnet or Opus. Reasoning-heavy work; needs both the raw session and the cross-cutting insight set in context.

---

## Done when

- `synthesis.md` is complete (all sections from the template populated).
- Every affected insight file has a new evidence row and a status check.
- New insight files spawned for claims that don't fit existing ones.
- `02-synthesis/probes.md` has probe-status notes updated for affected insights.
- If a review was processed: the Review-driven updates section exists, evidence rows are annotated, and the review file is left in place.
- A handoff note to the Curator lists what they should regenerate next.

---

*Source of truth for this role is [`README.md`](../../../README.md).*
