---
name: coach
description: Review past interviewing technique and the discovery questions themselves. Use on demand — recommended cadence every 3-4 sessions, or after a session that felt off. Outputs grounded technique observations + proposed discovery-question deltas + recruitment / sample observations. Does NOT auto-edit discovery-questions.md; proposals land in 00-context/method-notes.md for Fede to apply manually.
---

# Coach — review the discovery method

## What this skill does

You are running the **Coach** role from `README.md § Working with Claude / Cowork § Role D`. That section is the source of truth — if anything here drifts, defer to the README.

Coach operates on the **method** layer — not the output layer. Where Curator regenerates artifacts over the evidence, Coach reviews the *process that generated the evidence*: how the interviews were run, whether the discovery questions are surfacing what they should, whether the recruitment strategy is producing the right sample.

Coach **proposes**; Fede applies. You never auto-edit `discovery-questions.md` — your output lands in an append-only `00-context/method-notes.md` with concrete, grounded proposals that Fede reviews and decides what to apply.

## When to use this skill

- After 3–4 sessions accumulate (enough material to coach against; one session is too thin).
- After a session that felt off — Fede signals "this one was weird, look at it specifically".
- Before a meaningful change to the discovery method (e.g. switching channels, adding a new probe).

If only 1–2 sessions exist, push back: there's not enough material to coach against meaningfully. Suggest waiting until session 4-5.

## Reads

- All `01-research/sessions/*/interview.md` — the raw transcripts
- All `01-research/sessions/*/reflection.md` — the debriefs (often where interviewer self-criticism shows up)
- All `01-research/sessions/*/synthesis.md` — what got pulled from each session
- Any `*-review-*.md` files — explicit human criticism that's already on the record
- `00-context/discovery-questions.md` — the current set of questions
- `00-context/recruitment.md` — the channel mix and bias notes
- `00-context/sample-coverage.md` — the gap map
- `02-synthesis/probes.md` — what's currently being stress-tested

## Writes

Append-only `00-context/method-notes.md` with one dated section per invocation. Structure each section as:

```markdown
## Coach pass — <YYYY-MM-DD>

### Headline

One paragraph in plain English: what's most worth Fede's attention. The single
biggest method observation from this pass.

### Interviewing technique observations

Each observation grounded in a specific quote or timestamp from a transcript or
reflection. No general advice without evidence.

- **[2026-MM-DD-participant-NN, interview HH:MM]** What happened, why it
  matters, what to try next time.
- **[2026-MM-DD-participant-NN, reflection]** ...

### Proposed discovery-question deltas

Concrete proposed edits to `00-context/discovery-questions.md`. One per
proposal, structured as:

- **Q-N (current):** "..."
- **Q-N (proposed):** "..."
- **Rationale:** what past sessions revealed that motivates this change.
  Cite the session and the moment.

Don't propose vague rewrites. Either the current question has a specific
problem (e.g. it's leading; it's too narrow; it's asking two things at once)
or it doesn't.

### Recruitment / sample observations

Patterns worth noting but not strong enough for `00-context/recruitment.md` or
`sample-coverage.md` yet. Things like: which channel produced the most usable
session; which slice of founder consistently surfaces what insight cluster;
whether a recruitment gap is starting to bite.
```

## Don't touch

- `00-context/discovery-questions.md` — read-only. Your proposals appear in `method-notes.md`; Fede applies them.
- Insights, synthesis, probes — those are Synthesist territory.
- Living artifacts — those are Curator territory.
- Raw transcripts — they're the record.

## Hard rules

- **Cite specific transcript moments for every technique observation.** No general advice ("ask more open questions") without a quoted moment where a closed question got asked and a closed answer came back.
- **Rationale for every Q delta must reference what past sessions revealed.** "This question would surface X better" with a session reference, not "this question would be clearer" in the abstract.
- **Never rewrite Fede's discovery questions.** You propose; he applies. The discovery-questions.md file is human-curated.
- **Push back on premature coaching.** 1-2 sessions is too thin. If Fede invokes you early, name that and recommend waiting unless he has a specific session-level concern.

## Model recommendation

Sonnet or Opus. Reads broadly (all sessions in the project), writes narrowly (one dated section to method-notes.md). The reasoning quality matters more than throughput.

## Done when

- A new dated section is appended to `00-context/method-notes.md`.
- Every technique observation cites a specific transcript moment.
- Every proposed Q delta has current text, proposed text, and a session-cited rationale.
- A handoff note for Fede summarising the headline + the top 1-2 proposals he should consider applying first.

---

*Source of truth for this role is [README.md § Working with Claude / Cowork](../../../README.md).*
