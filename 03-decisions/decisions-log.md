# Decision log

> [!NOTE]
> **What this file is.** An append-only log of every meaningful decision, newest at top. This is how future-you (and the team) understands *why* things are the way they are.

---

## Chain-of-evidence rule

> [!IMPORTANT]
> Every decision must cite ≥1 piece of upstream evidence: an insight ID, an opportunity, a test, or a specific session or file. Process decisions (about how the knowledge base itself works) can cite the README or template they're changing.

If a decision can't cite anything, either it's premature or there's missing evidence work to do first.

---

## *Seed entry — adapt or replace when specialising the template*

### YYYY-MM-DD — Adopt the four-role discipline and human-review convention

- **Decision:** Use four working roles — Intake, Synthesist + Reconciler, Curator, Coach — each as a Claude Code skill under `.claude/skills/`. Treat human reviews of any artifact as first-class evidence: recorded as `<artifact-base>-review-<YYYY-MM-DD>.md` sibling to the artifact, reconciled by the Synthesist as a second pass.
- **Context:** Template-level decision. Captures the principle that the cost of a fresh agent is the number of files it has to read in order to write one file correctly. Splitting writes across four roles keeps reads bounded and lets the right model size do each job. Reviews keep human-in-the-room signal accountable in the same way raw transcripts already are.
- **Evidence:** `README.md` (Working with Claude / Cowork; Human reviews are first-class evidence); `.claude/skills/{intake,synthesise,curate,coach}/SKILL.md`.
- **Owner:** Template author.
- **Revisit when:** Friction emerges with role boundaries, or the project's discovery pattern doesn't fit the four-role split.

---

## Decision entry template

Copy this block per decision.

```
### YYYY-MM-DD — [short decision title]

- **Decision:** what was decided.
- **Context:** what prompted it.
- **Evidence:** ≥1 insight ID, opportunity, test, session, or — for process decisions — README or template. Required.
- **Alternatives considered:** what else was on the table and why it lost.
- **Owner:** who made the call.
- **Revisit when:** condition that would reopen this, if any.
```
