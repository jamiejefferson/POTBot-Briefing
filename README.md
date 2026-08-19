# POTBot-Briefing

**The problem:** when a human uses a bot to create content they must present to others, they haven't done the thinking — so they don't know the detail or the choices made, can't be sure the original challenge was fully answered, and struggle when challenged.

**The thesis:** this is a solved problem. Ministers, barristers, CEOs, commanders, and press secretaries have all spent decades being briefed to stand behind work other people did. This repo researches how they do it, extracts the mechanisms that transfer, and packages them as a working skill.

## Contents

| Path | What it is |
|---|---|
| [WHITEPAPER.md](WHITEPAPER.md) | **Start here.** The full write-up with citations: the need, the cross-domain research that drives the solution, the seven convergent mechanisms, and how the skill works. |
| [skill/potbot-briefing/](skill/potbot-briefing/) | **The skill.** An interactive briefing any chat can run: triage → briefing pack → pre-brief → teach-back gate → murder board (voice-preferred) → sign-off and room kit. `SKILL.md` plus reference files for the pack templates, interrogation/teach-back protocols, murder-board method, and condensed evidence base. |
| [research/01-politics-and-government.md](research/01-politics-and-government.md) | Ministerial submissions, red boxes, lines to take, PMQs prep, murder boards, debate stand-ins, the PDB briefer, press-secretary binders, speechwriting, failure cases. |
| [research/02-law.md](research/02-law.md) | Witness prep vs coaching, *R v Momodou* familiarisation, the brief to counsel, SCOTUS moot prep, deposition rules, the 30(b)(6) corporate designee, expert witnesses, failure modes from the bench. |
| [research/03-business.md](research/03-business.md) | Earnings-call Q&A banks, murder boards, consulting pre-wiring/dry runs/appendix culture, the Pyramid Principle, Amazon narratives and PR/FAQs, completed staff work, board prep, media training. |
| [research/04-military-and-intelligence.md](research/04-military-and-intelligence.md) | Completed staff work, BLUF and briefing types, confirmation brief/backbrief, commander's intent, PDB briefer discipline, red teaming/premortems, ROC drills, decision briefings. |
| [research/05-cognitive-science.md](research/05-cognitive-science.md) | The evidence base: illusion of explanatory depth, protégé effect, retrieval practice, desirable difficulties, generation effect, cognitive offloading/automation bias in the GenAI era, accountability norms. |

## The idea in one sentence

A briefing bot must be an **interrogating tutor, never a narrator**: it forces choices, ships the work inside an interrogation-ready pack, lets the human interrogate it, verifies understanding by closed-book teach-back, attacks the human harder than the real audience will (out loud, where possible), equips them for the edge of their knowledge — and only then invites them to sign.

## Installing the skill

Copy `skill/potbot-briefing/` into your skills directory (e.g. `~/.claude/skills/`), or install the packaged `.skill` file. Then in any chat: *"brief me on this"*, *"murder board me"*, or just produce a deliverable you'll have to present — the skill offers itself.
