# Review of cpca-kb-discovery

**Reviewer:** Claude (AI workflow engineer + user researcher lens)
**Date:** 2026-05-26
**Scope:** Full repo at HEAD `e81b852` — README, all skills, 00-context, 02-synthesis templates, 01-research scaffolding, syntax-guide, settings.

---

## Context

You asked for an honest read on a discovery knowledge-base system you've built, from two perspectives: AI workflow engineer and user researcher. The repo is a generic, specialisable template (no real sessions yet) with a four-role agent split — Intake, Synthesise, Curate, Coach — backed by a layered directory model (00-context → 01-research → 02-synthesis → 03-decisions → 04-outputs) and a chain-of-evidence rule that runs from raw session through to readout.

This document is the review itself plus a small, prioritised set of suggested adjustments — not an implementation plan, because the right next step depends on which (if any) of these critiques land for you.

---

## Headline

This is unusually good. It's the cleanest agent-workflow design I've seen for qualitative research, and the research methodology underneath it is more rigorous than most teams ever achieve. The two innovations that genuinely impress me:

1. **Status by disconfirmation, not by source count.** The hunch → emerging → strong → contested ladder requires *deliberate falsification attempts*, not accumulated agreement. This is the right discipline and it's almost never applied in practice.
2. **The "Sources at regeneration" footer as a drift sensor.** If the footer's session/insight list doesn't match current state, the artifact is automatically stale. Most systems let drift accumulate silently. This one surfaces it.

The bigger architectural call — splitting work into four roles by *context required to write the file correctly* rather than by *capability* — is right, and the README articulation of that principle ([README.md:182-184](../README.md#L182-L184)) is the cleanest one-paragraph statement of multi-agent design I've read.

The honest caveat: nothing has been run yet. You have an extremely thoughtful design that hasn't met a real participant. Several of the choices below will only be testable once you've done five or six sessions.

---

## What's strong (AI workflow lens)

- **Role boundaries are stated as "reads / writes / does NOT touch."** Every skill enforces this. ([intake/SKILL.md](../.claude/skills/intake/SKILL.md), [synthesise/SKILL.md](../.claude/skills/synthesise/SKILL.md), etc.) This is the right shape for keeping agent context lean and making failures legible.
- **"Additive only on claims" rule** ([synthesise/SKILL.md:86-92](../.claude/skills/synthesise/SKILL.md#L86-L92)) directly defends against the most common LLM failure mode: silent rewrites that look like improvements. Pairing it with `via review <date>` annotations on review-driven changes gives you an audit trail by default.
- **Coach is read-only on discovery-questions.md.** Proposals land in [method-notes.md](../00-context/method-notes.md) for you to apply manually. This is the right human-in-the-loop boundary — the discovery method shouldn't drift based on agent feedback alone.
- **Model assignment per role is sensible.** Intake = Haiku/light Sonnet (clerical), Synthesist = Sonnet/Opus, Curator = Opus, Coach = Sonnet/Opus. Matches reasoning load.
- **The rhythm includes "what to defer if you fall behind"** ([rhythm.md:51-61](../00-context/rhythm.md#L51-L61)), in order of safety. I have never seen this in a research playbook. It is the difference between a system that works in theory and a system that survives a busy week.

## What's strong (research lens)

- **Chain of evidence is the backbone, end-to-end.** Opportunities cite insight IDs, story map cites JTBD IDs, JTBD cites insight or session IDs, insights cite session evidence rows. You cannot float a claim. This is uncommon and load-bearing.
- **Consent is captured per participant on eight dimensions with conservative defaults** ([consent-log.md:1-57](../00-context/consent-log.md#L1-L57)). GDPR-aligned and ethically right.
- **Human reviews are first-class evidence**, recorded as raw transcripts (not summaries) and reconciled through a second Synthesist pass. This preserves nuance and prevents the reviewer from becoming an unaccountable editor.
- **Probes are explicit, prioritised, and trimmed.** [probes.md](../02-synthesis/probes.md) keeps the disconfirmation list to top 2-3. This is realistic.
- **Personas, journey, story map, themes, opportunities are all regenerated, not edited.** Treating them as views over the evidence rather than authored documents is the right call.

---

## Concerns and gaps

Ordered roughly by how much they'd matter once you start running sessions.

### 1. There are no worked examples

Everything is a template. Not a single populated insight, synthesis, or living artifact. The first time you (or anyone else) tries to invoke `/synthesise` on a real session, you'll be reasoning about what the artifacts *should* look like from the templates alone.

**Suggested fix:** Before specialising for CPCA, write one fictional but plausible session end-to-end — interview.md, reflection.md, synthesis.md, two derived insights, one probe, footer-stamped themes.md after curation. Keep it as `_EXAMPLE-session/` so it's visibly not real. It will sharpen the templates and surface ambiguities you can't see from the schema alone.

### 2. The Curator does editorial work without enough scaffolding

Regenerating themes, personas, and journey stages requires interpretation: which insights cluster, where the persona boundaries fall, what the journey stages even are. The skill says "group by what they have in common" and "regenerate from insights" but doesn't enumerate principles or require the Curator to surface its grouping choices.

**Risk:** Two runs of the Curator on the same data can produce different theme groupings, and you won't have a way to compare them.

**Suggested fix:** Add a "Grouping rationale" section to themes.md and personas.md that the Curator must write before the artifact itself — one sentence per cluster explaining what unifies it, citing the insight IDs that drove the boundary. Drift then becomes legible rather than invisible.

### 3. The `strong` status threshold may be impractical at small sample

`strong` requires "a deliberate disconfirmation attempt — a participant picked because they were likely to contradict." In civic / advisory / founder-discovery work, you often can't pick who agrees to talk. Forcing this strict reading means no insight ever reaches `strong`, which devalues the ladder.

**Suggested fix:** Loosen to a *boundary-case* test rather than a *suspected-contradictor* test. `strong` = at least one participant whose profile (sector, stage, geography, funding, etc.) is the slice *most likely* to break the claim — even if you didn't pre-suspect they would. Same discipline, looser causal language.

### 4. Coach proposals are easy to lose

Coach appends to [method-notes.md](../00-context/method-notes.md) and you apply changes manually. After 4-5 Coach passes the file gets long, and proposals from session 3 may quietly age out without ever being applied or rejected.

**Suggested fix:** Add a status flag to each proposal block: `proposed` / `applied YYYY-MM-DD` / `rejected YYYY-MM-DD (reason)`. Either you or the Coach (read-only on Q file, write to its own notes) keeps the bookkeeping. Without this, method-notes becomes a graveyard.

### 5. No saturation principle

[rhythm.md](../00-context/rhythm.md) says "after 8-10 sessions, draft opportunities and write a readout" but doesn't articulate when the sample is sufficient. Saturation can come earlier or later than 8.

**Suggested fix:** Add to rhythm.md: "Insight saturation is provisionally reached when the last 3 sessions added no new insights and challenged no existing ones. Note in the next Coach pass; do not stop on this alone." Keep it a *signal*, not a *stopping rule*, because counter-examples lurk in unrecruited slices.

### 6. No path forward when an insight goes `contested`

System says "mark contested, don't rewrite." Good — but then what? In practice, contested insights either need splitting (different mechanisms in different slices) or qualifying (true under condition X, not Y). Without a path, contested items accumulate and the ladder stalls.

**Suggested fix:** In synthesise/SKILL.md, add a small playbook: when marking contested, the Synthesist proposes 1-3 candidate resolutions (split into sub-claims, qualify with conditions, demote to hunch) in a `## Proposed resolution` block inside the insight file. You pick one in the next pass. The proposal isn't an edit to the claim — it's a question for the human.

### 7. The settings.local.json points to the wrong path

[.claude/settings.local.json](../.claude/settings.local.json) references `/Users/fedecarbo/Downloads/cpca-discovery/` but the project lives in `/Users/fedecarbo/Documents/cpca-kb-discovery/`. Looks like a copy from another working copy.

**Suggested fix:** Trivial — either delete or update the `additionalDirectories` entry.

### 8. Sample design is implicit

[sample-coverage.md](../00-context/sample-coverage.md) records coverage *after the fact* but there's no upfront sampling plan: who do you intend to talk to, what slices matter, why. This usually lives as a one-page document in serious research.

**Suggested fix (lightweight):** Add a "Target sample" section at the top of sample-coverage.md — the slices you decided up front matter, with reasoning. Then the coverage matrix tracks delivery against intent, not just emergent description.

### 9. Interviewer-bias check missing

If the interviewer is a domain insider — and in CPCA-style discovery they often are — framing biases the data. The system has Coach but no specific instruction to scan for leading questions, premature solutioning, or insider shorthand in transcripts.

**Suggested fix:** Add to coach/SKILL.md, under "Interviewing technique observations": "Check for leading questions, premature solution language from the interviewer, and insider shorthand the participant may have echoed without owning. Cite the transcript line."

---

## Suggested next steps (prioritised)

Do these in order; stop wherever the cost-benefit stops feeling right.

1. **Fix the settings path** ([.claude/settings.local.json](../.claude/settings.local.json)). 2 minutes.
2. **Write the worked example session.** One fictional `_EXAMPLE-session/` populated end-to-end so the templates are concrete. Half a day.
3. **Add the "Grouping rationale" requirement** to themes.md and personas.md templates, and add a paragraph to [curate/SKILL.md](../.claude/skills/curate/SKILL.md) requiring it before regeneration. 30 minutes.
4. **Loosen the `strong` definition** to boundary-case in [synthesise/SKILL.md](../.claude/skills/synthesise/SKILL.md), [probes.md](../02-synthesis/probes.md), and the README chain-of-evidence section. 20 minutes.
5. **Add status flags to Coach proposals.** Update [coach/SKILL.md](../.claude/skills/coach/SKILL.md) and [method-notes.md](../00-context/method-notes.md) header. 15 minutes.
6. **Add contested-resolution playbook** to [synthesise/SKILL.md](../.claude/skills/synthesise/SKILL.md). 20 minutes.
7. **Saturation signal in rhythm.md.** 10 minutes.
8. **Run the first real session and review what hurt.** Most of the above will only be validated by friction.

The first session is the real test. Several of these recommendations will look obviously wrong once you've actually invoked the pipeline on a real interview, and that's fine — the design is good enough that the only thing left is to find out where it bends.
