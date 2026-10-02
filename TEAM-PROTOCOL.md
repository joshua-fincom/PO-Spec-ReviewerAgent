# Where decisions live

The agent enforces a checklist. This document is the working agreement that makes the
checklist stick. Without it the same questions get asked again on the next card.

## The rule

> **Any decision that affects more than one card is documented at Feature level, in the
> PRD. Not in a card comment.**

A card states the outcome and links the PRD section. The PRD holds the reasoning.

## Why

A decision settled in a comment on one story is invisible to its siblings. The next story
re-opens it, the dev asks again, and the PO answers again — often differently. In the
298-card retrospective behind this agent, that pattern was the single most repeatable
source of avoidable dev questions.

Writing it once at Feature level means every sibling card inherits it.

## For POs

**When a decision gets made** — whether in refinement, in a Jira thread, or in a call:

1. Write it into the **parent Feature's PRD**, under a dated decision entry: what was
   decided, why, and what it rules out.
2. In the card, state the **outcome** in the AC and link the PRD section.
3. Do **not** paste the reasoning into the card, and do not mirror it across sibling
   cards. One edit, one place — otherwise the copies drift and nobody knows which is live.

**Then tell the devs it happened.** A PRD edit is silent — nobody watches Confluence. Post
**one comment on the parent Feature**:

- one line saying what was decided
- a link to the PRD section holding the reasoning
- an @-mention of the assignees on the affected child cards

One comment on the Feature, not one per child. Do not rewrite the children's descriptions,
and do not paste the reasoning into the comment — it links, it does not duplicate.

If the ruling changes what a specific card must now do, update **that card's AC** to the
new outcome. That is the only place the outcome gets restated, and it still links the PRD.

**When you hit a question while drafting**, work this order before raising it:

| | Look here |
|---|---|
| 1 | This card — description, every AC, the comments |
| 2 | Sibling cards under the same parent Feature |
| 3 | The parent Feature |
| 4 | The Feature's PRD |

If the answer exists only in a card comment, that is a gap: lift it into the PRD now. The
agent flags this as **G20**.

**Before endorsing to For Tech Review**, run the agent on your own card. Fix every BLOCKER.
The point is that the dev receives a card with nothing left to ask — a review that happens
after a dev picks it up has already cost the back-and-forth it was meant to prevent.

## For developers

**Read the Feature's PRD before raising a question on a card.** If the answer is already
there, say so in the thread and ask the PO to link it from the card. That is a one-line
fix — not a decision that needs re-making.

**When a decision gets made in a card thread — point it back to the Feature.** A ruling
that stays in a comment is lost to every sibling card. Ask the PO to write it into the PRD,
or say in the thread which PRD section should carry it.

**Preflight findings that are product calls belong in the PRD too.** If a preflight
resolves something the card left open — a default, a boundary, an empty-state decision —
that is now a product decision made in a comment. Flag it so it gets recorded at Feature
level, otherwise the next card in the Feature inherits nothing.

## The test

Before closing any decision, ask: **if a different person picked up the sibling card
tomorrow, would they find this?**

If the only answer is "they'd have to read the comments on a different ticket", it is not
documented yet.
