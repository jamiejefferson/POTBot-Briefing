# Standing behind work you didn't do: a synthesis

**The problem.** When a human uses a bot to create content they must present to others, three things go wrong: they don't understand the detail, they don't know what choices were made (or what was rejected), and they can't be sure the original challenge was fully answered. So when challenged, they struggle — and everyone in the room can tell.

**The reframe.** This is not a new problem, and it is largely a solved one. Ministers defend policies researched by civil servants. Barristers argue cases built by solicitors. CEOs defend numbers produced by finance teams. PDB briefers present intelligence they didn't analyse. US law even has a formal rule — FRCP 30(b)(6) — under which one person must testify, under oath and hostile questioning, to *everything an entire organisation knows*, and courts accept this as legitimate **provided a structured education process happened first**. The principal–staffer relationship has spent a century building machinery for exactly this handover. The bot is a new staffer; the machinery transfers.

This document synthesises research across five domains — [politics & government](research/01-politics-and-government.md), [law](research/02-law.md), [business](research/03-business.md), [military & intelligence](research/04-military-and-intelligence.md), and [cognitive science](research/05-cognitive-science.md) — into the mechanisms every domain independently converged on, and what they imply for a skill.

---

## The core insight: ownership is not authorship

No domain requires the presenter to have done the work. Every domain replaces authorship with a different, achievable standard:

- **The expert witness standard:** you needn't have run every model, but you must be able to *defend every number* — a verification duty, not an authorship duty.
- **The completed staff work signature test (US Army, 1942):** *"Would you sign this and stake your professional reputation on it being right? If not, send it back."* Signing is the ownership transfer; presenting is signing.
- **The 30(b)(6) standard:** "I didn't do this work" is not a disqualifier — it's an engineering problem solved by scoped, structured education.
- **The emerging AI-governance standard:** "human reviewed it" is procedural theater; "human can explain and defend it under challenge" is the real bar.

The consistent diagnosis of failure is also identical everywhere: **the well-briefed principal knows the reasoning and the weak points; the poorly-briefed one has memorized conclusions.** Memorized conclusions shatter at the first follow-up, because interrogators — journalists, judges, analysts, board members — are all trained to ask the same question: *why?* (See Diane Abbott's LBC interview, Chloe Smith on Newsnight, the appellate judge's "Where is that in the record?", the executive's "what's under that number?")

## Why bots make this worse than human staffers

The cognitive science explains why the bot version of the problem feels more acute than the human version, and it comes down to four compounding effects:

1. **Polished output is a fluency trap.** Reading smooth prose produces the *feeling* of understanding with none of the substance (illusion of explanatory depth; Bjork's fluency illusion). Re-reading it — the natural instinct — measurably doesn't help (retrieval practice beats re-reading ~61:40 at one week).
2. **The human made no choices.** A human staffer's principal was in meetings, set direction, saw drafts. A bot user often sees only the final artifact. The generation effect says what you chose you remember and own; a fait accompli transfers nothing.
3. **The bot's confidence suppresses challenge.** Trust in AI is the strongest predictor of *not* thinking critically about its output (Microsoft/CMU CHI 2025), and people skip verification when they feel unqualified to judge.
4. **Nothing arrives with the work.** A ministerial submission ships with a defensive annex; a brief to counsel ships with a chronology and numbered sources. Bot output typically ships naked — no decision log, no confidence marks, no anticipated questions.

The good news from the same literature: the harm is a function of interaction design, not of AI itself. The same model that damages learning as a ghostwriter *improves* it as a tutor (Bastani et al., PNAS 2025). The whole design question is which mode the bot operates in at handover time.

## The seven convergent mechanisms

Every domain independently invented some version of all seven. This convergence is the strongest evidence we have that they work.

### 1. Pull ownership upstream — decisions, then edits

Speechwriters start with an intent conversation ("what's the story, and why are *you* the one telling it?") and end with the principal crossing out full pages; Obama edited nearly all of 3,477 speeches. Ministers physically mark up every red-box submission. Military decision briefings show labeled assumptions and evaluation criteria so the commander can audit the reasoning and *own* the decision, not rubber-stamp it. The cognitive science mechanism is the generation effect: contribution creates ownership.

**Translation:** during drafting, the bot should force real forks (framing A vs B, which recommendation, which number leads) and log the choices; before any briefing, the human must do a mark-up pass — change things, cut things. A human who has edited the output can honestly claim it; one who has only read it cannot. The decision log becomes the skeleton of the later briefing.

### 2. The deliverable ships with an interrogation-ready pack

The universal artifact set, assembled from the ministerial submission, the brief to counsel, the IR Q&A bank, Amazon's PR/FAQ, the consulting appendix, and intelligence tradecraft:

- **The intent layer** (commander's intent / message house): purpose, top-line claim, 3–4 pillars with proof points, definition of success. Small enough to memorize; what lets the presenter improvise when Q&A goes off-script.
- **The pyramid** (Minto): answer-first hierarchy where each layer answers the "why?" of the layer above — a literal map of anticipated questions, defensible from any entry point.
- **The decision log**: what was chosen, *what was considered and rejected, and why*. "What did you consider and reject?" is a standard hostile question and unanswerable without this.
- **The coverage map**: the original brief/challenge decomposed into its parts, each mapped to where it's answered — directly closing the "do I have faith everything was fully answered?" gap.
- **The provenance map**: every load-bearing claim one hop from its source. "Where did that number come from?" is the killer question in every domain, and one confident false citation poisons everything.
- **Known / assessed / unknown marks with calibrated confidence** (intelligence discipline): what is verified fact, what is the bot's judgment, what is open — so the human never silently upgrades "likely" to "definitely" in transmission.
- **The defensive annex**: the 5–10 hardest questions with answer *frameworks* (positions + evidence, never scripts), split into "lines to take" (volunteer) and "if asked" (deploy only under challenge), plus red lines (never say).
- **The load-bearing facts card**: the 2–3 numbers that must be cold. (Abbott's interview died on exactly one uninternalized figure.)

### 3. The pre-brief: interrogate the producer

PDB briefers are pre-briefed *by the authoring analysts* on the reasoning chain before the President hears a word; red-box submissions get a private-secretary cover note; counsel rebuilds the case from the solicitor's chronology. The document is never the product — the conversation about it is.

**Translation:** the human interrogates the bot about its own output before anyone else can: why this conclusion, what evidence, what would change your mind, what's the strongest counterargument, where are you least sure. The bot answers as the analyst, and gaps found here become pack updates.

### 4. Verify understanding by generation, not recognition

The military backbrief: the subordinate re-briefs the plan in their own words (comprehension), then briefs *how they'll execute it* (reasoning). Teaching-based learning (protégé effect, *g* ≈ 0.66 for self-explanation) and the IOED literature agree: forced explanation both builds understanding and — crucially — *calibrates confidence*, because the human feels exactly where the explanation runs dry.

**Translation:** a teach-back gate. The human explains the work to the bot playing the naive stakeholder, closed-book. Retrieval-style questions on the load-bearing facts. Not passed = not briefed, and the failed spots define the next round.

### 5. Adversarial rehearsal, harder than the real thing

Murder boards for Supreme Court nominees, PMQs prep with an aide "throwing abuse" as the Leader of the Opposition, debate stand-ins who *become* the opponent, Georgetown's moots for nearly every SCOTUS argument, the consulting dry run, Klein's premortem. Two distinct payoffs: it surfaces the gap between recognition and recall while being wrong is still cheap, and it *stress-inoculates* — the real room feels easier than the rehearsal. John Roberts prepped ~1,000 questions to field ~100, and drilled his argument from shuffled index cards so command never depended on sequence.

**Translation:** the bot role-plays the *specific* audience (questions come from interests, and interests are knowable — model the actual people in the room), asks harder questions than they will, follows up on every "why", and enters the material in random order. Scale rounds to stakes.

### 6. Procedures for the edge of knowledge

Every domain teaches that disasters come from bluffing past the boundary, not from admitting it. Deposition rules make "I don't know" a trained, legitimate, credibility-*enhancing* move. Media training teaches bridging (answer briefly → bridge → safe ground). The press secretary's tabbed binder makes visible reliance on notes compatible with authority — what's in the binder is safe; anything else is a pre-approved "I'll come back to you." 30(b)(6) scopes the topics: full depth inside a declared perimeter beats shallow universal coverage.

**Translation:** the briefing explicitly defines the perimeter (what the human is answerable for, what gets deferred and to whom), rehearses the exit moves, and produces a legitimate-to-use tabbed crib sheet for the room.

### 7. A sign-off gate that means something

The chain ends with the signature test, gated on demonstrated performance (teach-back passed, murder board survived), not attestation. "I read it" is theater; "I explained it under attack" is ownership. Courts sanction the unprepared designee "as a witness who never showed up" — the accountability is real because the test was.

## The skill, in one sentence

**A briefing bot must be an interrogating tutor, never a narrator:** it forces choices during drafting, ships the work inside an interrogation-ready pack, lets the human interrogate it, verifies understanding by teach-back, attacks the human harder than the real audience will, equips them for the edge of their knowledge — and only then invites them to sign.

The draft skill implementing this is at [skill/SKILL.md](skill/SKILL.md). Two calibrations matter in practice:

- **Scale to stakes.** A stand-up update needs the intent layer and three questions; a board pitch needs the full pack and a murder board. Every domain scales this way (4–6 hours of prep per earnings call; five weeks for a SCOTUS argument).
- **Respect the human's time asymmetry.** The bot does everything it can alone (the pack, the question bank, the audience model); the human's scarce minutes go only where the science says transfer actually happens — choosing, editing, explaining, being questioned.

## Failure modes the skill must avoid

- **Becoming a script factory.** Every domain insists on frameworks over scripts; verbatim answers crack under the first follow-up. The bot must brief positions and proof points, and refuse requests to "just write my answers."
- **Unsucceedable difficulty.** Desirable difficulties only work when the learner can succeed; quizzing a novice on trivia produces frustration, not ownership. Scaffold context first, then test.
- **Theater sign-off.** If the teach-back and murder board are skippable, the whole thing degrades to a checkbox — the exact "procedural theater" the accountability literature warns about.
- **Coaching over the line.** The legal distinction matters ethically here too: the process should build the human's genuine command of real content, never fluent delivery of claims they can't verify. If the pack's provenance map has holes, the fix is to fix the content, not rehearse around it.
