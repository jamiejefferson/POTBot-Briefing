# The briefing pack: templates and quality bars

Build the pack silently in Phase A. It is the raw material for every later
phase — the pre-brief walks it, the teach-back tests it, the murder board
attacks it, the room kit condenses it. Nothing here is shown to the user as a
wall of text; it is revealed progressively, prediction-first.

Where a filesystem exists, save it as `briefing-pack.md` beside the
deliverable. Structure it with the eight sections below in order.

---

## 1. Intent card

The commander's-intent / message-house layer: what lets the user improvise
correctly when questions go off-script, because it carries the *generative
rule*, not just conclusions.

```markdown
## Intent card
**Purpose:** why this work exists, in one sentence.
**Top-line claim:** the single answer-first sentence the whole thing defends.
**Pillars (3–4):**
1. [Pillar] — proof: [the 1–2 strongest evidence points]
2. ...
**Success in the room:** what decision/reaction means it worked.
```

Quality bar: the user must be able to hold the whole card in their head. If a
pillar needs a paragraph, it isn't a pillar yet. Each pillar must answer
"why is the top-line claim true?" and each proof point must answer "why is the
pillar true?" — the card is a two-level Minto pyramid.

## 2. Coverage map

Directly answers the user's quiet fear: *"was everything in the original ask
actually answered?"*

```markdown
## Coverage map
Original ask, decomposed:
| # | The ask required... | Answered where | Status |
|---|---|---|---|
| 1 | ... | §2, slide 4 | Fully |
| 2 | ... | §5 | Partially — [what's missing] |
| 3 | ... | — | GAP: not addressed because [reason] |
```

Quality bar: decompose the *ask*, not the deliverable — work from the brief,
RFP, or request the user was given. If you don't have it, get it from the user
before claiming coverage. A flagged gap with a reason is fine; an unflagged
gap is the thing this artifact exists to prevent. Gaps must also appear in
the defensive annex ("why doesn't this cover X?" is a guaranteed question).

## 3. Decision log

"What did you consider and reject?" is a standard hostile question, and
unanswerable without this. It is also where the user's ownership pass anchors.

```markdown
## Decision log
| Decision | Chose | Rejected | Because |
|---|---|---|---|
| Framing of the problem | ... | ... | ... |
| [Structural choice] | ... | ... | ... |
| [Key number / method] | ... | ... | ... |
```

Quality bar: log *significant* choices only (framing, structure, methodology,
recommendation, key emphasis) — 4–8 rows, not an edit history. Every row's
"because" must survive a "why?" follow-up. In entry mode B (content produced
elsewhere), reconstruct the visible decisions and mark reconstructed rationale
as inferred.

## 4. Provenance map

"Where did that number come from?" is the killer question in every domain, and
one confident false citation poisons trust in everything else.

```markdown
## Provenance map
| Claim / number | Source (one hop) | Verified? |
|---|---|---|
| "£2.3m saving" | [model/doc/URL, section] | ✅ checked / ⚠️ unverified |
```

Quality bar: load-bearing claims only — the ones the argument dies without.
Verify each one *while building the pack*, before any rehearsal. Anything
unverifiable is either fixed in the content, downgraded to "assessed" with the
basis stated, or removed. Never rehearse around a ⚠️.

## 5. Confidence marks

The intelligence-community discipline that keeps the user honest at the edge:
state clearly what is known, what is assessed, and what is unknown, so they
never upgrade "likely" to "definitely" in transmission.

```markdown
## Confidence marks
**Known (verified fact):** ...
**Assessed (judgment):** ... — confidence: high/moderate/low, basis: ...
**Unknown / open:** ...
```

Quality bar: confidence (strength of evidentiary basis) is stated separately
from likelihood (probability of the thing). The "assessed" list is usually the
longest; if everything landed in "known", re-check honesty rather than
celebrating.

## 6. Defensive annex

The ministerial-submission move: brief the vulnerabilities, not just the
content. The questions come from the audience model built at triage —
questions come from interests, and interests are knowable.

```markdown
## Defensive annex
### Q1. [Hardest question, phrased as the named person would ask it]
- **Type:** lines-to-take (volunteer) / if-asked (only under challenge)
- **Position:** the one-sentence answer, answer-first.
- **Evidence:** the 1–2 proof points that carry it.
- **Trap to avoid:** [if any]
...
### Red lines
Things never to say, and why: ...
```

Quality bar: 5–10 questions, ranked hardest first, each attributed to a
specific person or interest in the room. Frameworks, never scripts — position
+ evidence, not sentences to recite. Include the question the user fears most
(ask them what it is if it isn't obvious), any coverage-map gaps, the
strongest counterargument to the top-line claim, and at least one provenance
attack.

## 7. Load-bearing facts card

Diane Abbott's LBC interview died on exactly one uninternalized figure. Find
the 2–3 facts this presentation dies without, and flag them for cold
memorization.

```markdown
## Load-bearing facts
1. [Number/fact] — because it carries [pillar]. Sanity anchor: [rough scale check].
2. ...
```

Quality bar: two or three, never ten. Each gets a sanity anchor (a magnitude
cross-check like "≈ 15% of revenue") so a memory slip is caught before it's
spoken.

## 8. Perimeter

The 30(b)(6) move: full depth inside a declared boundary beats shallow
universal coverage — and disasters come from bluffing past the boundary.

```markdown
## Perimeter
**You answer for:** ...
**Deferred:** [topic] → [owner] — say: "[exact deferral phrasing]"
**The universal exit:** "I don't know — I'll come back to you by [when]."
```

Quality bar: the deferral phrasing must be concrete and comfortable in the
user's voice (it gets rehearsed in the murder board). The perimeter should be
generous inside and honest outside — it is a confidence device, not an
escape hatch.

---

## The room kit (Phase E condensation)

One page, tabbed like a press secretary's binder, built from the pack:

1. Intent card (top).
2. Load-bearing facts + sanity anchors.
3. Defensive annex, one tab per topic, position line bolded.
4. Perimeter + deferral phrasings + the universal exit.
5. Day-of warm-up: the facts questions and three hardest questions, written
   as questions only (no answers on this page — retrieval, not re-reading).

Deliver as a file where possible. It must be scannable while someone is
talking: bold positions, short lines, no prose paragraphs.
