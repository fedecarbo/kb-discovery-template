# Review — [artifact name]

> [!NOTE]
> **What this file is.** A human review of an agent-produced artifact. Reviews are first-class evidence in this project — agents synthesise, but humans in the room (or with domain knowledge) catch what an agent can't. Recorded as a transcript so the raw human signal stays intact, like the interview transcripts.

- **Date:** *YYYY-MM-DD.*
- **Reviewed by:** *name(s).*
- **Reviewing:** *path to artifact, e.g. `01-research/sessions/2026-MM-DD-participant-NN/synthesis.md`.*

> [!IMPORTANT]
> **Filename convention.** Save this file sibling to the artifact being reviewed, named `<artifact-base>-review-<YYYY-MM-DD>.md`. Multiple reviews of the same artifact accumulate (different dates; never overwrite).

---

## Headline

*One paragraph in plain English: what shifted after this review. Written so a reader skimming weeks later understands the upshot without reading the full transcript. If nothing meaningful shifted, say so explicitly — "review confirmed the synthesis as-is; no action items".*

---

## Action items

Concrete edits the Synthesist second pass should make to the artifact (or to dependent artifacts like the insight files). Keep each one specific enough to apply without re-reading the transcript.

- [ ] *Specific edit needed to `synthesis.md` or insight `I-XXX`.*
- [ ] *Specific edit needed to `02-synthesis/probes.md` or `01-research/method/recruitment.md`.*
- [ ] *…*

---

## Transcript

Raw transcript of the review conversation. Don't polish — capture pauses, corrections, and offhand observations. Timestamps optional but useful.

```
[HH:MM] <name>: <what they said>
[HH:MM] <name>: <…>
```

---

## How this gets reconciled

After saving this file:

1. Re-invoke the **Synthesist** (`.claude/skills/synthesise/`). It scans for `*-review-*.md` files alongside artifacts in scope.
2. Synthesist appends a `## Review-driven updates (<YYYY-MM-DD>)` section to the affected `synthesis.md`, or annotates evidence rows in insight files, with each change tagged `via review <YYYY-MM-DD>`.
3. This review file stays in place as an audit trail.

> [!IMPORTANT]
> **The Synthesist does not silently overwrite first-pass claims.** Every change carries its `via review` provenance.
