# Discovery project: knowledge base

> The index. Read this first. It explains the project, how the folders work, the
> synthesis model, transcript verification, the disconfirmation discipline, the
> evidence chain, the human-review convention, and the four working roles.

---

## What this is

A generic discovery-research knowledge base for early-stage product discovery.
Specialise it by replacing the placeholders below — region, authority, support
ecosystem, domain — with your own. The structure, conventions, and roles work
for any discovery project that wants to keep evidence accountable to itself.

A discovery effort for **[DISCOVERY_DOMAIN]** in the **[AUTHORITY_NAME]**
region. We're researching how **[USERS]** currently **[CURRENT_BEHAVIOUR]**,
so we can design **[INTENDED_OUTCOME]** that gets the right expertise to them
at the right moment. See `00-context/product-vision.md` and
`00-context/problem-statement.md` for the framing.

- **Current phase:** *(set to: scoping / interviewing / synthesising / writing-up)*
- **Last updated:** *(date)*

---

## The shape of the work

Raw inputs stay raw; meaning is built on top and always traces back down.

| Folder | Layer | What lives here |
|---|---|---|
| `00-context/` | Context | Stable background: vision, problem, discovery questions, personas, `glossary.md` (confirmed proper nouns), `sample-coverage.md` (who we've heard from), `recruitment.md` (funnel), `consent-log.md` (per-participant permissions), `rhythm.md` (default cadence), `method-notes.md` (Coach observations). **Read before anything else.** |
| `01-research/` | Inputs + Facts | One folder per session: raw transcripts, a per-session synthesis, and an optional interview guide. Plus testing and other feedback. Reviews live sibling to the artifact being reviewed (e.g. `synthesis-review-<date>.md`). |
| `02-synthesis/` | Insights + Views | Atomic insights (`insights/` with `INDEX.md` manifest), `probes.md` (active disconfirmation list), `jobs-to-be-done.md`, `opportunities.md`, plus living artifacts (themes, journey, story map, stakeholder map). |
| `03-decisions/` | Conclusions | Decision log: what we chose, when, why, with evidence citation. |
| `04-outputs/` | Communication | Generated artifacts shaped for an audience: presentation structures, readouts, briefings, show-and-tell notes. Markdown by default; built from the evidence layer on request, not hand-maintained. |

---

## The chain of evidence

**Every link must cite the one above it.** This is the difference between a knowledge base and a vibes document.

```
session → fact → insight → JTBD → story map → opportunity → test → decision
   ↓        ↓       ↓        ↓         ↓           ↓          ↓        ↓
session   quote   I-00X    J-F/A    cite ≥1      cite ≥1    cite ≥1  cite ≥1
folder   in     evidence   cites    J-ID or      insight   opportunity evidence
       synthesis  table   ≥1 I-ID   insight       ID          ID       item
```

- Every **insight** cites the sessions it draws on (in its evidence table).
- Every **JTBD** in `jobs-to-be-done.md` cites ≥1 insight ID or session ID, or is explicitly marked `assumption`.
- Every **story map** activity cites ≥1 JTBD entry (J-ID). Steps without a J-ID either need a new JTBD entry or should be cut.
- Every **opportunity** in `opportunities.md` cites ≥1 insight ID.
- Every **test** in `01-research/testing/` cites ≥1 opportunity.
- Every **decision** in `03-decisions/decisions-log.md` cites ≥1 piece of upstream evidence (insight, opportunity, test, session, or, for process decisions, the README or template being changed).

If a link can't cite the one above it, it isn't ready. There's missing evidence work to do first.

---

## Sessions are bundled

Each session is a small folder: the interview, the debrief, the synthesis, and (from session 2 onward) the interview guide.

```
01-research/sessions/YYYY-MM-DD-participant-NN/
├── interview.md     ← raw interview transcript
├── reflection.md    ← post-interview debrief (observed context)
├── guide.md         ← the question script we used (optional but recommended)
└── synthesis.md     ← STAGE 1: this session, distilled from BOTH transcripts
```

Copy `_TEMPLATE-session/` and rename `YYYY-MM-DD-participant-NN/` for each new one.

---

## Two kinds of synthesis

**Atomic insights** (`02-synthesis/insights/`) are additive: one idea per file, each *accrues* evidence as sessions come in. You never rewrite them; they gain weight. A one-line-per-insight manifest lives in `02-synthesis/insights/INDEX.md` — read that first.

**Living artifacts** are regenerated views over the atomic layer, *not* hand-maintained:

- `journey-map.md`: current-state experience across users
- `story-map.md`: future-solution backbone (downstream of the journey)
- `stakeholder-map.md`: who's in the ecosystem and how they connect
- `themes.md`: emergent clusters of insights
- `personas.md`: refined from evidence
- `opportunities.md`: needs and problems worth pursuing, rooted in insights

The rule: **insights and sessions are the source of truth; living artifacts are rebuilt on demand** so they never silently drift. When context grows, ask the agent to regenerate them. Don't edit findings into them by hand. Every regenerated artifact carries a "Sources at regeneration" footer that lists the sessions and insights in scope — if that footer is stale, regenerate before relying on it.

Cadence for regeneration lives in `00-context/rhythm.md`.

---

## Human reviews are first-class evidence

Synthesis is a claim about what was heard. The humans who were in the room — or who know the field — catch things an agent can't: a misread silence, a contradicted observation, a domain detail. Reviews are how that signal gets back into the knowledge base.

**The convention:** any artifact (a session synthesis, an individual insight, a living artifact like the journey map) can be reviewed. The reviewer records the review as a transcript — same format as an interview, because the project already treats raw human speech as the ground truth — sibling to the artifact being reviewed, named `<artifact-base>-review-<YYYY-MM-DD>.md`.

Example paths:

```
01-research/sessions/YYYY-MM-DD-participant-NN/synthesis-review-YYYY-MM-DD.md
02-synthesis/insights/I-006-short-slug-review-YYYY-MM-DD.md
02-synthesis/journey-map-review-YYYY-MM-DD.md
```

Multiple reviews of the same artifact accumulate (different dates, never overwrite). Use `01-research/sessions/_TEMPLATE-review.md` as the starting template — it has a Headline section (plain-English upshot for scannability), an Action-items list, and the raw transcript.

**Reconciliation:** the Synthesist role (see below) runs as a *second pass* when a review file exists. It scans for `*-review-*.md` files alongside artifacts in scope, ingests them, and writes a `## Review-driven updates (<YYYY-MM-DD>)` section into the affected `synthesis.md` (or annotates insight evidence rows). First-pass claims are never silently overwritten — every change carries a `via review <YYYY-MM-DD>` annotation, so the audit trail survives.

---

## Insights graduate by disconfirmation, not just accumulation

Insight statuses are not just "how many sessions support this":

- **hunch**: 1 supporting source. No disconfirmation attempted.
- **emerging**: 2–3 supporting sources AND ≥1 session that *could* have contradicted it but didn't (the probe was live going in).
- **strong**: 4+ supporting sources AND ≥1 deliberate disconfirmation attempt (a participant picked because they were *likely* to contradict) that failed.
- **contested**: ≥1 session that materially contradicts the claim. Don't rewrite; flag, and either narrow the claim or split it.

The active list of "what to stress-test next, and who could do it" lives in `02-synthesis/probes.md`, regenerated from the insights folder.

---

## Sample coverage shapes what insights mean

An insight is only as general as the sample it was drawn from. `00-context/sample-coverage.md` shows the *shape* of who we've heard from (stage, background, sector, geography, demographic). `00-context/recruitment.md` shows the *flow*: who's been approached, who declined, what channels we've tried. Before recruiting the next participant, look at both: the most valuable next interview is usually the one that fills a gap, not the one that's easiest to book.

---

## Transcripts get verified, never overwritten

Auto-transcripts mangle proper nouns. A confidently wrong name can corrupt an insight, so:

1. **The raw transcript stays untouched**: it's the record. Corrections live in the session's `synthesis.md` under **Transcription flags**.
2. The agent **normalises** high-confidence errors in interpretation (noting the original) and **flags**, rather than guesses, anything uncertain, especially proper nouns an insight depends on.
3. You **resolve the flags in the reflection meeting**, while it's fresh.
4. Confirmed terms **graduate to `00-context/glossary.md`**, so future transcript interpretation auto-corrects and only *new* unknowns get flagged. It compounds.

(Note: "auto-correct" happens in the agent's *reading* and the *synthesis*. The raw transcript files themselves are never edited.)

---

## Consent is captured per session

`00-context/consent-log.md` tracks what each participant agreed to across several dimensions (recording, internal use, named, re-contact, prototype testing, anonymised quotes, named quotes, public use). Defaults are conservative. If a dimension wasn't explicitly agreed, treat it as **no**. Use the intake checklist in that file at the start of every interview.

---

## The two workflows (the engine)

### A. New session comes in

Drop both transcripts in a new session folder, then:

1. Write `synthesis.md`: distill both transcripts; normalise or flag transcription.
2. **Reconcile** against `insights/`: reinforce one (add the session ID), contradict one (flag it as contested), or spawn a new insight.
3. **Update `00-context/sample-coverage.md`** with this session's slice.
4. **Update `00-context/consent-log.md`** with what the participant agreed to.
5. **Update `02-synthesis/probes.md`** if this session changed any insight's disconfirmation state.

### B. Step back and synthesise

On the rhythm defined in `00-context/rhythm.md`:

1. **Regenerate** the living artifacts from the current insights and sessions.
2. Promote insights whose evidence and disconfirmation now qualify them.
3. Refresh `probes.md` and `opportunities.md`.
4. When ready, generate a readout for **[STAKEHOLDER]**.

---

## Working with Claude / Cowork

The read-and-write surface clusters into four roles. Each role names what an agent reads, what it writes, and what model size fits. Calling them out keeps each agent's context lean, lets the right model size do each job, and means a fresh agent (or a fresh human) can orient inside the role rather than trying to hold the whole project at once.

The cost of a fresh agent isn't the number of files in the project — it's the number of files an agent has to *read in order to write one file correctly*. Intake's writes don't need the insight set. Curator's writes don't need raw transcripts. Only the Synthesist needs both, and only for one bounded call. Coach reads broadly but writes narrowly. Split the writes, and the reads shrink to fit each role.

Each role is also a Claude Code skill — invoke as `/intake`, `/synthesise`, `/curate`, `/coach`. The skills live in `.claude/skills/` and reference this README as source of truth.

### Role A — Intake

Runs the moment a new session lands. Clerical and pattern-matching; no insight-level reasoning.

- **Reads:** the two raw transcripts, `00-context/glossary.md`, the session templates.
- **Writes:** the session folder (`interview.md`, `reflection.md`, the transcription-flags section of `synthesis.md`), updates to `00-context/sample-coverage.md` and `00-context/consent-log.md`, additions to the glossary review queue.
- **Doesn't:** reason about insights. No reconciliation; no probes; no spawning.
- **Model:** Haiku or light Sonnet.
- **Example invocation:** *"Intake the new session at `01-research/sessions/YYYY-MM-DD-participant-NN/`. Normalise known terms from the glossary; flag anything uncertain. Update sample-coverage and consent-log. Don't touch insights."*

### Role B — Synthesist + Reconciler

The reasoning-heavy role. Runs once per session, after Intake. Holds the cross-cutting view — never split this role further. **Also runs as a second pass** when a `*-review-*.md` exists alongside any artifact in scope; reconciles synthesis + insights against the human review (additive, never overwriting first-pass claims).

- **Reads:** the Intake output, all of `02-synthesis/insights/` (starting with `INDEX.md`), `02-synthesis/probes.md`, the discovery questions. On every invocation, scans for `*-review-*.md` files alongside artifacts in scope.
- **Writes (first pass):** the rest of `synthesis.md` ("What we heard", "What the reflection added", "Standout moments", "How this changes the insights", "Effect on probes"); evidence rows and status updates in affected insight files; new insight files when a claim doesn't fit any existing one; status notes in `probes.md` for affected insights only.
- **Writes (second pass — review reconciliation):** a `## Review-driven updates (<YYYY-MM-DD>)` section appended to `synthesis.md`; corrected or added evidence rows in affected insight files tagged `via review <YYYY-MM-DD>`; status notes if the review shifts confidence. Never silently overwrites first-pass claims.
- **Doesn't:** regenerate living artifacts. Touches each insight only if the session bears on it.
- **Model:** Sonnet or Opus.

### Role C — Curator

Runs periodically per `00-context/rhythm.md`, not per session, and before any **[STAKEHOLDER]**-facing output. Operates over the evidence layer — doesn't touch raw transcripts.

- **Reads:** all of `02-synthesis/`, all of `00-context/`, recent sessions.
- **Writes:** regenerated living artifacts (`themes.md`, `journey-map.md`, `story-map.md`, `stakeholder-map.md`, `personas.md`, `opportunities.md`) — *populate each one's "Sources at regeneration" footer with the session and insight IDs in scope*; a regenerated `02-synthesis/insights/INDEX.md` whenever the insight set changes (new file, status change, evidence-row added); a trimmed `probes.md` (top 2–3 right now, not per-insight detail); a refreshed `Current state of play` in this README; surfaced flags for what's stale or pending human input.
- **Doesn't:** touch raw transcripts, individual insight files, or the discovery method itself (Coach territory).
- **Model:** Opus.

### Role D — Coach

Operates on the *method* layer (not the output layer). Runs on demand — recommended cadence: every 3–4 sessions, or after a session that felt off. Reviews past interviewing technique and the discovery questions themselves. Outputs proposals; doesn't auto-edit discovery questions.

- **Reads:** all `01-research/sessions/*/interview.md` + `reflection.md` + `synthesis.md`; any `*-review-*.md` files; `00-context/discovery-questions.md`; `00-context/recruitment.md`; `00-context/sample-coverage.md`; `02-synthesis/probes.md`.
- **Writes:** append-only `00-context/method-notes.md` with a dated section per invocation, structured as: Headline + Interviewing technique observations (each grounded in a specific quote or timestamp) + Proposed discovery-question deltas (current → proposed + rationale; one per proposal) + Recruitment / sample observations.
- **Doesn't:** auto-edit `discovery-questions.md` (read-only); touch insights, synthesis, or living artifacts.
- **Model:** Sonnet or Opus.

---

## Current state of play

_Last updated: <date>._

> This section is a *delta from default* — what's abnormal, pending, or about to bite. The current state itself lives in the source-of-truth files (pointer index below). Don't duplicate it here; that's a tax that compounds.

**Where we are.** *(One short paragraph: the latest session, what it added or changed, the single most important constraint on the next move. Filled in by the Curator after each rhythm step-back.)*

**Pending human input.**
- *(Specific items only the user can decide or confirm.)*

**Pointer index.** Where to read the actual current state:

| For | Read |
|---|---|
| Insights | `02-synthesis/insights/INDEX.md` first (one-line manifest), then individual files |
| Sample shape, recruitment gaps | `00-context/sample-coverage.md`, `00-context/recruitment.md` |
| Probes / what to stress-test next | `02-synthesis/probes.md` |
| Glossary + review queue | `00-context/glossary.md` |
| Consent | `00-context/consent-log.md` |
| JTBD | `02-synthesis/jobs-to-be-done.md` |
| Living artifacts (themes, journey, story, stakeholders, personas, opportunities) | `02-synthesis/` — *regenerated per `00-context/rhythm.md`* |
| Coach observations + proposed discovery-question deltas | `00-context/method-notes.md` |
| Human reviews of any artifact | `<artifact>-review-<YYYY-MM-DD>.md` (sibling to the artifact); template at `01-research/sessions/_TEMPLATE-review.md` |
| Decisions and process conventions | `03-decisions/decisions-log.md` |

---

## Specialising this template

This template is region-, authority-, and domain-agnostic. To specialise for a real project:

1. Replace placeholders throughout:
   - `[DISCOVERY_DOMAIN]`, `[AUTHORITY_NAME]`, `[REGION_NAME]`, `[GROWTH_HUB_NAME]`, `[USERS]`, `[CURRENT_BEHAVIOUR]`, `[INTENDED_OUTCOME]`, `[STAKEHOLDER]`
2. Populate `00-context/problem-statement.md`, `00-context/product-vision.md`, `00-context/discovery-questions.md`.
3. Log the specialisation as a decision in `03-decisions/decisions-log.md`.
4. Treat improvements you make during real research as candidates to backport to the template — one-way sync: project → template, never reverse.
