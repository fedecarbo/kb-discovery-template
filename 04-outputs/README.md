# 04-outputs — communication artifacts

> [!NOTE]
> **What this folder is.** Things shaped **for an audience** — not sources of truth, but deliverables built from them. Show-and-tells, discovery readouts, stakeholder briefings, product vision structures.

The distinction from `02-synthesis/` is intent. Living artifacts there are the evidence layer — rebuilt on demand, never hand-edited. Files here are one-time communication pieces, generated on request.

---

## What lives here

- **Presentation structures:** slide-by-slide outlines in markdown, ready to build into Google Slides.
- **Discovery readouts:** narrative summaries of what we've learned, shaped for a specific audience.
- **Briefings or one-pagers:** focused documents for a specific stakeholder or meeting.
- **Show-and-tell notes:** running structure or talking points for a session.

---

## What doesn't live here

- Raw transcripts → `01-research/sessions/`.
- Atomic insights → `02-synthesis/insights/`.
- Living artifacts (journey map, personas, etc.) → `02-synthesis/`.
- Decisions → `03-decisions/`.

---

## Format

Plain markdown by default. Presentation structures are written as slide outlines — headings for slides, bullets for content — so they're easy to drop into Google Slides manually. No `.pptx` files.

---

## Naming convention

```
YYYY-MM-DD-[type]-[audience-or-occasion].md
```

Examples:

- `2026-05-25-readout-cpca-session1.md`
- `2026-06-10-show-and-tell-team.md`
- `2026-07-01-vision-structure-internal.md`

---

## Traceability

> [!IMPORTANT]
> Claims in any output should trace back to an insight ID, JTBD ID, or session ID where possible. An output that floats free of the evidence layer is a vibes document. It will drift.
