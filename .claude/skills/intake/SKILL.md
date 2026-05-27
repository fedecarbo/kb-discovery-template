---
name: intake
description: Process a freshly-recorded interview into a session bundle. Use when a new participant has been interviewed and the raw transcripts have been dropped into a session folder. Normalises terminology against the glossary, flags transcription uncertainties (especially proper nouns), and updates sample-coverage + consent-log + glossary review queue. Does NOT reason about insights or touch the synthesis layer.
---

# Intake — process a new session

> [!NOTE]
> You are running the **Intake** role from `README.md § Working with Claude — the four roles § Role A`. That section is the source of truth — if anything here drifts, defer to the README.

## What this skill does

Intake is the clerical, pattern-matching pass on a freshly-arrived session. You normalise known terms, flag uncertain ones, and update the project's coverage, consent, and glossary state.

> [!IMPORTANT]
> You do **not** reason about insights, reconcile against the insight set, or write the cross-cutting parts of `synthesis.md`. That's the Synthesist's job.

---

## When to use this skill

- A new session folder exists at `01-research/sessions/YYYY-MM-DD-participant-NN/` containing at least `interview.md` and `reflection.md` (and optionally `guide.md`).
- The transcripts are raw — possibly auto-transcribed, with mangled proper nouns.
- No synthesis has been written yet, or only the template scaffold exists.

If `synthesis.md` already has content beyond the Transcription flags section, you've arrived after Intake should have run. Stop and ask whether to redo Intake or hand off to Synthesist.

---

## Reads

- `01-research/sessions/<this-session>/interview.md`
- `01-research/sessions/<this-session>/reflection.md`
- `01-research/sessions/<this-session>/guide.md` (if it exists)
- `01-research/method/glossary.md` — confirmed-term dictionary and review queue
- `01-research/sessions/_TEMPLATE-session/synthesis.md` — section structure
- `01-research/method/sample-coverage.md` — coverage matrix shape (so your row matches)
- `01-research/method/consent-log.md` — dimensions to capture

## Writes

In the session folder:

- `synthesis.md` — only the top of the file (metadata block + **Transcription flags** section). Leave "What we heard", "How this changes the insights", "Effect on probes" empty for the Synthesist.

In `01-research/method/`:

- `sample-coverage.md` — append one row to the coverage matrix; tick any newly-covered slices in the gap lists. Don't trim or rewrite existing rows.
- `consent-log.md` — append the participant's consent row (dimensions confirmed via the consent form or interview opener).
- `glossary.md` — for confirmed terms heard in the session, add to the dictionary. For uncertain terms (especially proper nouns an insight might depend on), add to the **review queue** with a flag.

## Doesn't touch

- `02-synthesis/insights/` — no evidence rows, no new files, no status updates.
- `02-synthesis/probes.md`, `02-synthesis/jobs-to-be-done.md`, living artifacts.
- The raw transcripts themselves (`interview.md`, `reflection.md`). They are the record. Corrections live in `synthesis.md`'s Transcription flags section.

> [!IMPORTANT]
> **One exception.** Redact the participant's literal name as described below. That is the only substitution Intake makes to the raw transcripts.

---

## Redact the participant's name

Replace the participant's real name with their participant ID (`P01`, `P02`, etc., from the session folder name) everywhere it appears in `interview.md` and `reflection.md`. Catch greetings, self-introductions, and any time the interviewer addresses them by name.

The real name is provided in the invocation prompt, or can be inferred from speaker labels in an auto-transcript (e.g. `Speaker 1: Jane`).

> [!NOTE]
> If `01-research/method/consent-log.md` shows the participant agreed to **Named in internal docs**, you can skip this redaction.

Don't redact other people mentioned, organisations, or locations in this pass. If broader PII redaction becomes needed, the user will say so.

---

## How to handle transcription flags

Apply the project rule (see README § "Transcripts get verified, never overwritten"):

1. **Normalise high-confidence errors** in your reading and in the synthesis. Note the original in the **Normalised** subsection — `"garbled" → **Correct term**`.
2. **Flag low-confidence uncertainties** in the **Needs confirmation** subsection. Don't guess proper nouns an insight might depend on.
3. Add confirmed terms to `01-research/method/glossary.md`; add uncertain terms to its review queue.

> [!IMPORTANT]
> The raw transcript files are never edited.

---

## Model recommendation

Haiku or light Sonnet. Pattern-matching workload; no cross-cutting reasoning required.

---

## Done when

- The participant's real name no longer appears in `interview.md` or `reflection.md` (unless consent permits being named).
- `synthesis.md` has the metadata block and Transcription flags filled in.
- `01-research/method/sample-coverage.md` has the new session's row plus any newly-covered slices ticked.
- `01-research/method/consent-log.md` has the participant's consent dimensions row.
- `01-research/method/glossary.md` has any confirmed new terms added; uncertain terms parked in the review queue.
- A handoff note to the Synthesist mentions what's still to do.

---

*Source of truth for this role is [`README.md`](../../../README.md).*
