# POTBot Briefing: standing behind work you didn't do

*Why humans can't defend AI-generated content, what a century of principal–staffer practice teaches us about fixing it, and how the POTBot Briefing skill works.*

---

## Summary

When a human uses AI to create content they must present to others, three things go wrong: they don't understand the detail, they don't know what choices were made or what was rejected, and they can't be sure the original ask was fully answered. When challenged, they struggle — and everyone in the room can tell.

This is not a new problem, and it is largely a solved one. Ministers defend policies researched by civil servants; barristers argue cases built by solicitors; CEOs defend numbers produced by finance teams; intelligence briefers present analysis they didn't write. Every one of these fields has spent decades building machinery for exactly this handover, and — remarkably — they all converged on the same small set of mechanisms. Cognitive science explains why those mechanisms work and why their absence around AI output makes the problem acute.

POTBot Briefing is a skill that packages that machinery into an interactive briefing any chat can run: it builds an interrogation-ready pack around the work, has the human interrogate and edit it, verifies understanding through a closed-book teach-back, rehearses them against a murder board harder than the real room (by voice where possible), and gates sign-off on demonstrated command rather than attestation.

This paper covers the need (§1), the precedent (§2), the research-derived mechanisms (§3), how the skill implements them (§4), and the design constraints that keep it honest (§5). Full domain studies with sources are in [`research/`](research/).

---

## 1. The need

### 1.1 The presentation gap is real and measurable

The failure mode is already visible at scale. BetterUp and Stanford's 2025 study of AI-produced work products ("workslop") found 40% of workers receive AI output that masquerades as good work; each instance costs the receiver roughly two hours, and crucially, *senders are judged less capable and less trustworthy* as a result ([HBR, Sept 2025](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity)). Organisational policy is converging on the counter-norm: a 2026 study of open-source contribution guidelines found 74% of AI policies require human oversight, with Selenium's stating it plainly — "You are the author. You must read, review, and understand all AI-assisted output before requesting review" ([arXiv](https://arxiv.org/pdf/2605.16706)). Governance writing warns that a human "in the loop" who cannot genuinely evaluate the output is *procedural theater*, not accountability ([TechPolicy.Press](https://www.techpolicy.press/ai-efficiency-can-undermine-accountability-even-with-humans-in-the-loop/)).

The standard that is emerging everywhere is not "a human reviewed it" but **"a named human can explain and defend it under challenge."** Nothing in mainstream AI tooling currently gets a person to that standard.

### 1.2 Why AI makes this worse than the human-staffer version

Executives have always presented work their teams did. Four compounding effects make the AI version harder:

1. **Polished output is a fluency trap.** People systematically mistake the *feeling* of understanding for its substance — the illusion of explanatory depth: self-rated understanding collapses when people are forced to actually explain ([Rozenblit & Keil 2002](https://onlinelibrary.wiley.com/doi/10.1207/s15516709cog2605_1)). Smooth, fluent input inflates the feeling further while adding nothing durable ([Bjork Lab, desirable difficulties](https://bjorklab.psych.ucla.edu/research/)) — and re-reading, the natural remedy, measurably doesn't help: retrieval practice beats re-reading roughly 61% vs 40% recall at one week ([Roediger & Karpicke 2006](https://journals.sagepub.com/doi/10.1111/j.1467-9280.2006.01693.x)).
2. **The human made no choices.** A staffer's principal sat in meetings, set direction, marked up drafts. An AI user often sees only the finished artifact. The generation effect says what you produce or choose you remember and own; what is handed to you, you don't ([Slamecka & Graf 1978](https://notes.andymatuschak.org/zWvCEwYz4Uv1dMHXynq3H5w); [2025 replication](https://link.springer.com/article/10.1186/s41235-025-00645-2)). The MIT "cognitive debt" study found LLM-assisted writers reported the lowest ownership of their own essays and often *couldn't quote them minutes later* ([Kosmyna et al. 2025](https://arxiv.org/abs/2506.08872) — a small-sample preprint, cited here as suggestive).
3. **The AI's confidence suppresses challenge.** Trust in AI is the strongest predictor of *not* thinking critically about its output, and workers skip verification when they feel unqualified to judge ([Microsoft/CMU, CHI 2025](https://dl.acm.org/doi/abs/10.1145/3706598.3713778); see also automation complacency and bias, [Parasuraman & Manzey 2010](https://journals.sagepub.com/doi/10.1177/0018720810376055)).
4. **Nothing arrives with the work.** A ministerial submission ships with a defensive annex of vulnerabilities; a brief to counsel ships with a chronology and numbered sources. AI output typically ships naked — no decision log, no confidence marks, no anticipated questions.

The decisive finding is that the harm is a function of *interaction design*, not of AI itself: in a randomised study of ~1,000 students, unrestricted GPT access boosted practice performance 48% but **cut** later exam scores 17%, while the same model constrained to tutor mode (hints, not answers) erased the harm entirely ([Bastani et al., PNAS 2025](https://www.pnas.org/doi/10.1073/pnas.2422633122)). The entire design question is which mode the AI operates in at handover time.

---

## 2. The precedent: this is a solved problem

### 2.1 Ownership is not authorship

No field that manages this problem requires the presenter to have done the work. Each replaces authorship with a different, achievable standard:

- **The expert-witness standard.** Testifying experts routinely rely on staff-run models, yet must "be prepared to defend every single number" ([ACTEC](https://actecfoundation.org/podcasts/witness-depositions-of-valuation-experts/)) — a *verification* duty, not an authorship duty. Adopting a report by signature without genuine review is the recognised malpractice ([Hofstra Law Review](https://www.hofstralawreview.org/wp-content/uploads/2020/05/48.1.bb_.4.greenbaum.pdf)).
- **The 30(b)(6) standard.** US federal procedure requires an organisation to produce one witness to testify to *everything the organisation knows*. Courts accept this as fully legitimate — provided a structured education process happened first (document review, interviews "from mailroom to senior management") — and sanction an unprepared designee "as a witness who never showed up" ([ABA](https://www.americanbar.org/groups/tort_trial_insurance_practice/resources/brief/archive/speak-yourself-30b6-deposition/); [LegalClarity](https://legalclarity.org/rule-30b6-depositions-notice-prep-and-sanctions/)). "I didn't do this work" is not a disqualifier; it is an engineering problem with a known solution.
- **The completed-staff-work standard** (US Army, 1942) supplies the exit test, applied here with the AI as staff and the human as chief: *"Would you sign this and stake your professional reputation on it being right? If not, take it back and work it over"* ([govleaders.org](https://govleaders.org/completed-staff-work.php)).

### 2.2 The consistent diagnosis of failure

Across every field, prepared and unprepared principals fail the same way: **the well-briefed principal knows the reasoning and the weak points; the poorly-briefed one has memorised conclusions** — which shatter at the first follow-up, because every trained interrogator's follow-up is "why?". Diane Abbott's 2017 LBC interview collapsed on one uninternalised number ([BBC](https://feeds.bbci.co.uk/news/election-2017-39775693)); Chloe Smith's Newsnight collapse came from being sent out on a decision without its rationale ([LibDemVoice](https://www.libdemvoice.org/ldvideo-chloe-smiths-carcrash-fuel-duty-newsnight-interview-29172.html)); the appellate advocate's nightmare is "Where is that in the record?" with no answer ([ABA](https://www.americanbar.org/groups/litigation/committees/appellate-practice/articles/2018/winter2018-how-to-confront-your-worst-fears-about-appellate-oral-argument/)). Challengers don't test everything — they pull one thread deeply, and the question is whether it snaps.

---

## 3. The research: seven convergent mechanisms

Five parallel domain studies ([politics & government](research/01-politics-and-government.md), [law](research/02-law.md), [business](research/03-business.md), [military & intelligence](research/04-military-and-intelligence.md), [cognitive science](research/05-cognitive-science.md)) found that every field independently invented some version of all seven mechanisms below. That convergence — practitioners in unrelated traditions arriving at the same designs, each validated by the learning-science literature — is the strongest evidence available that they work.

### M1. Pull ownership upstream: decisions, then edits

Speechwriters open with an intent conversation and end with the principal crossing out pages — Obama edited nearly all of his 3,477 speeches ([Miller Center oral history](https://millercenter.org/the-presidency/presidential-oral-histories/cody-keenan-oral-history)); ministers physically mark up every red-box submission ([IfG](https://www.instituteforgovernment.org.uk/explainer/ministers-private-offices)); military decision briefings expose labeled assumptions and evaluation criteria so the commander audits the reasoning and *owns* the decision ([FM 6-0 briefing formats](https://www.globalsecurity.org/intell/library/policy/army/fm/34-80/appb.htm)). Mechanism: the generation effect — contribution creates ownership.

### M2. The work ships inside an interrogation-ready pack

The universal artifact set, assembled from the ministerial submission's "areas of vulnerability and the counter arguments" ([civilservant.org.uk](https://www.civilservant.org.uk/skills-briefing.html)), the brief to counsel's chronology and numbered sources ([Hancy](https://hancy.net/resources/briefing-a-barrister/how-to-brief-a-barrister/)), the IR Q&A bank ([ACCESS Newswire](https://www.accessnewswire.com/blog/the-earnings-call-preparation-checklist-for-ir-teams)), Amazon's self-interrogating PR/FAQ ([workingbackwards.com](https://workingbackwards.com/concepts/working-backwards-pr-faq-process/)), the Minto pyramid — a literal map of anticipated questions ([StrategyU](https://strategyu.co/pyramid-principle-partone/)) — and intelligence tradecraft's known/assessed/unknown discipline with calibrated confidence language ([Kent's Words of Estimative Probability](https://www.globalsecurity.org/intell/ops/probability.htm); ICD 203). The handover artifact is designed for *lookup under pressure*, not linear reading.

### M3. The pre-brief: interrogate the producer

PDB briefers are pre-briefed *by the authoring analysts* on the reasoning chain — tradecraft, sourcing, alternative views — before the President hears a word, with a closed feedback loop for follow-ups ([CIA](https://www.cia.gov/stories/story/a-day-in-the-life-of-a-pdb-briefer)). The document is never the product; the conversation about it is. Mechanism: elaborative interrogation — "why"-questions drive deep processing ([Dunlosky et al. 2013](https://journals.sagepub.com/doi/abs/10.1177/1529100612453266)).

### M4. Verify understanding by generation, not recognition

The military's confirmation brief and backbrief have the receiver re-brief the plan in their own words, then explain how they'll execute it ([CALL rehearsal doctrine](https://www.globalsecurity.org/military/library/report/call/call_98-5_rehears4.htm)) — you cannot re-express what you don't hold. Mechanisms: the self-explanation effect (g ≈ 0.66, [Bisra et al. 2018]) and the protégé effect — preparing to teach beats preparing to be tested ([Stanford AAA Lab](https://aaalab.stanford.edu/assets/papers/2009/Protege_Effect_Teachable_Agents.pdf)); and IOED calibration — the explainer *feels* exactly where their understanding runs dry, which recalibrates confidence durably ([Rozenblit & Keil](https://onlinelibrary.wiley.com/doi/10.1207/s15516709cog2605_1)).

### M5. Adversarial rehearsal, harder than the real thing

Murder boards for Supreme Court nominees ("if they make one 10-second mistake, it's all anyone will ever know about them" — [NBC on Kagan's prep](https://www.nbcnews.com/id/wbna37854053)); PMQs prep with an aide role-playing the Leader of the Opposition every week ([IfG](https://www.instituteforgovernment.org.uk/explainer/prime-ministers-questions-pmqs)); debate stand-ins who *become* the opponent ([NPR](https://www.npr.org/2012/09/30/162025715/to-prep-for-debates-stand-ins-take-the-stage)); Georgetown mooting nearly every SCOTUS argument ([Georgetown](https://www.georgetown.edu/news/moot-courtroom-us-supreme-court-prep/)); mock Q&A as IR's highest-ROI prep activity ([WeConvene](https://weconvene.com/earnings-call-preparation-checklist-ir-teams/)); Klein's premortem, raising failure-cause identification ~30% ([HBR](http://homepages.se.edu/cvonbergen/files/2013/01/Performing-a-Project-Premortem.pdf)). Two distinct payoffs: surfacing the recognition/recall gap while being wrong is cheap, and stress inoculation — the real room feels easier than the rehearsal. John Roberts prepared ~1,000 questions to field ~100 and drilled his argument from *shuffled index cards* so command never depended on sequence ([Virginia Appellate Law](https://www.virginiaappellatelaw.com/2011/05/articles/oral-argument/i-am-john-roberts-and-so-can-you-part-ii-oral-argument/)).

### M6. Procedures for the edge of knowledge

Deposition rules make "I don't know" a trained, legitimate, credibility-*enhancing* move ([ABA](https://www.americanbar.org/groups/young_lawyers/resources/tyl/practice-areas/deposition-preparation-four-simple-rules/)); media training's bridging provides a graceful path back to safe ground ([Media First](https://www.mediafirst.co.uk/blog/13-more-bridging-phrases-and-how-to-use-this-key-media-training-technique-well)); the press secretary's tabbed binder proves visible reliance on organised notes reads as command, not weakness ([WaPo](https://www.washingtonpost.com/opinions/2020/07/17/kayleigh-mcenany-watch-so-organized/)); 30(b)(6)'s noticed topics show that full depth inside a declared perimeter beats shallow universal coverage. Every field's disasters come from bluffing past the boundary, never from admitting it.

### M7. A sign-off gate that means something

The chain ends with the signature test, gated on *demonstrated* performance — teach-back passed, murder board survived — not attestation. "I read it" is procedural theater; "I explained it under attack" is ownership. The 30(b)(6) sanctions regime shows why the gate has teeth.

---

## 4. How POTBot Briefing works

The skill ([`skill/potbot-briefing/`](skill/potbot-briefing/)) turns the seven mechanisms into a staged interactive conversation. Its governing rule, from the tutor-vs-ghostwriter evidence: **an interrogating tutor, never a narrator** — every turn ends with one question, one choice, or one small task for the user, and content is revealed prediction-first, never dumped.

### Entry and triage

The skill triggers when a user must present or defend work they didn't fully author — or proactively, right after the AI produces a presentable deliverable. It first establishes **audience** (named people and their interests — questions come from interests, and interests are knowable), **exposure** (informing vs seeking a decision), and **stakes/time**, then declares one of three levels: a ~10-minute crib for low heat, the default 30–45-minute briefing, or full prep (60–90 minutes plus a day-of warm-up) for boards, pitches, and panels. Calibration is itself evidence-based: real-world prep scales the same way, from 4–6 executive hours per earnings call to five weeks for a SCOTUS argument. Two entry modes cover content the AI itself produced (it briefs from its own honest decision record) and content produced elsewhere (it reconstructs the pack and marks every untraceable claim *unverified* rather than guessing).

### Phase A — the briefing pack (M1, M2)

Built silently, saved as a file beside the deliverable, revealed only progressively. Eight artifacts: the **intent card** (purpose, top-line claim, 3–4 pillars with proofs — commander's intent plus message house); the **coverage map** (the original ask decomposed and mapped to where it's answered, gaps flagged — directly closing the "was everything fully answered?" fear); the **decision log** (chosen / rejected / because); the **provenance map** (every load-bearing claim one hop from its source, verified *before* rehearsal); **confidence marks** (known / assessed / unknown, confidence stated separately from likelihood); the **defensive annex** (5–10 hardest questions for *this* audience, answer frameworks split into lines-to-take vs if-asked, plus red lines); the **load-bearing facts card** (the 2–3 numbers that must be cold, each with a sanity anchor); and the **perimeter** (what the user answers for, what gets deferred, with rehearsed phrasing).

### Phase B — the guided walk-through (M1, M3)

The AI drives — the user should never face a blank page, because someone who doesn't yet understand the content cannot generate good questions about it. The rhythm is *walk → check → correct → move*: the AI talks the user through the argument in pyramid order (top-line claim, then each pillar — reasoning, evidence, rejected alternatives, confidence), in chunks of a few sentences, each ending in a check — a prediction before the next reveal, a "why"-probe, an application question, or a re-say in the user's own words. Challenges are *invited at specific moments* rather than left to the user ("before you trust that number — ask me where it comes from"; "this is the claim I'd attack — push me on it"), with the AI answering as the producer defending the work and fixing every exposed wobble visibly, which builds the user's licence to challenge. Woven through is the **ownership pass**: at least one genuine fork chosen ("lead with cost saving or risk retired — which is yours?") and one real edit — the top-line claim re-said in the user's own words and adopted; what they chose and edited, they will defend. Scaffolding keeps every difficulty winnable wherever the user lacks background.

### Phase C — the teach-back gate (M4)

Role-swap: the AI becomes a naive stakeholder; the deliverable is closed. The user explains the work from the top; the AI probes with innocent-but-deadly follow-ups ("sorry — why does that follow?", "where's that number from?"), then quizzes the facts card closed-book. Performance is scored against an open rubric (top-line and pillars, reasoning chain, choices, provenance, calibration, facts). **Not passed = not briefed** — failed rows loop back through a short re-brief and are re-tested. The confidence drop a user feels here is the illusion of explanatory depth being corrected, and the skill says so.

### Phase D — the murder board (M5, M6)

Only after a passed teach-back. The AI goes into role as the *actual* audience — named personas built from triage and the user's own intelligence about how each person pushes back — and is deliberately harder than the real room: a twelve-type question taxonomy (provenance attacks, why-chains, rejected alternatives, assumption flips, compound questions, interruptions, scope bait, the feared question, confidence probes, sanity checks, softball traps), entered in random order. **Voice is the preferred modality**: where the user's surface supports a voice conversation, the skill recommends running this phase spoken, because speaking is the performance modality, prevents composed-and-edited answers, and puts the stumble where it's informative; in text, it approximates pressure with short-clock, no-edit answers spoken aloud before typing. Between rounds the AI breaks role and gives rubric-scored feedback — what held, what cracked, and which answers were *borrowed rather than owned* — repairs the cracks, and re-attacks them from a different angle. Full prep adds a premortem, the shuffled-entry drill, round repeats to a clean pass, and an optional facilitator sheet so a human colleague can run the final round.

Throughout, the answer discipline from depositions and media training is taught and enforced: pause; answer the question asked first; one bridge to a pillar; never guess; deploy the perimeter deferral — and honest "I don't know — I'll come back to you" is *scored as a win*.

### Phase E — sign-off and the room kit (M6, M7)

The signature test, verbatim: "Would you sign this and stake your professional reputation on it being right?" Hesitation is routed to whichever phase can fix it; a theater "yes" after a failed teach-back is not accepted. The pack condenses into a one-page tabbed **room kit** (intent card, facts, annex tabs, perimeter — with the press-secretary rule: visible organised notes read as command), and a 5-minute **day-of warm-up** (spaced retrieval on the facts and three hardest questions) is scheduled or queued for the user's return — spacing plus retrieval being the highest-utility combination in the learning literature.

### Built-in resistance handling

The skill anticipates the three predictable objections: *"just write my answers"* (declined warmly — scripts shatter at the first follow-up; frameworks plus ten minutes of questioning offered instead); *"I've read it twice, I'm fine"* (the 90-second bet: three closed-book questions — a miss recalibrates better than any argument); *"there's no time"* (a minimum viable briefing — facts quiz, three hardest questions, perimeter — with what was skipped and the residual risk stated plainly, never silently degraded).

---

## 5. Design constraints and open questions

**What the skill must never become.** Four failure modes are designed against explicitly: the *script factory* (every domain insists on frameworks over scripts); *unsucceedable difficulty* (friction only helps when the learner can win through it — scaffold first, then test); *theater sign-off* (if the gates are skippable the whole process degrades to the checkbox it exists to replace); and *coaching over the line* (if briefing exposes an indefensible claim, the content is fixed, not the delivery — the boundary every profession's ethics draws).

**How to evaluate it.** End-of-session satisfaction is confounded by the very fluency illusion the skill exists to defeat — a bad version will feel great. Meaningful evals are delayed and behavioural: can the user answer the load-bearing questions cold the next day? Did the real Q&A go better? Automated tests can only check the opening behaviour (triage-first, no content dump, correct refusal of script requests); the skill ships with those in [`evals/evals.json`](skill/potbot-briefing/evals/evals.json).

**Open questions.** Whether the upstream lever (forcing choices *during* drafting — the strongest ownership mechanism of all) should also live in a companion convention for all content-producing work; how packs and warm-up state persist across sessions on surfaces without a filesystem; and whether the murder board should generate a facilitator pack by default so a human colleague always runs the final round at the highest stakes.

---

## Sources

Inline citations above link to primary sources. The five underlying domain studies, each with full sourcing:

1. [Politics & government](research/01-politics-and-government.md) — ministerial submissions, red boxes, lines to take, PMQs prep, murder boards, debate stand-ins, the PDB briefer, press-secretary binders, speechwriting, failure cases.
2. [Law](research/02-law.md) — witness prep vs coaching, *R v Momodou*, the brief to counsel, SCOTUS moot practice, deposition rules, Rule 30(b)(6), expert witnesses, failure modes from the bench.
3. [Business](research/03-business.md) — earnings-call Q&A banks, murder boards, consulting pre-wiring/dry runs/appendix culture, the Pyramid Principle, Amazon narratives and PR/FAQs, completed staff work, board prep, media training.
4. [Military & intelligence](research/04-military-and-intelligence.md) — completed staff work, BLUF and briefing types, confirmation brief/backbrief, commander's intent, PDB discipline, red teaming and premortems, ROC drills, decision briefings.
5. [Cognitive science](research/05-cognitive-science.md) — illusion of explanatory depth, self-explanation and protégé effects, retrieval practice, desirable difficulties, generation effect, cognitive offloading and automation bias in the GenAI era, accountability norms.
