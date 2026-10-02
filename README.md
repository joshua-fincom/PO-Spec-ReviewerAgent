# PO Spec Reviewer Agent

A pre-endorsement gate for Product Owners. Run it on your **own** card draft before
endorsing to For Tech Review, so developers receive a card with nothing left to ask.

## Why

Built from a retrospective of **298 Story/Task cards and 3,777 Jira comments** across the
Q4 2026 / Q1 2027 initiatives (October 2026).

| Finding | Number |
|---|---|
| Cards carrying a dev-written preflight pass that found product gaps | **57%** |
| Product gaps per card, where tabulated | **9.5** |
| Gaps decided by engineering and never escalated to Product | **80%** |
| Cards prescribing a mechanism the dev had to disprove | **27%** |

The 80% is the important one. Most gaps never arrive as a question — a developer simply
picks an answer and moves on. So "no open questions on the card" is not evidence the card
is complete, and the visible back-and-forth is only the surface of the cost.

Every check in the agent carries the count of real dev-raised gaps behind it. None were
invented from best-practice lists.

## Install

Drop `card-quality-reviewer.md` into your bot's agents directory:

```
.claude/agents/card-quality-reviewer.md     # project-scoped
~/.claude/agents/card-quality-reviewer.md   # available everywhere
```

Then invoke it: `"self-audit MP-1234"` · `"is this ready to endorse"` · `"review this card"`

**No Jira access in your bot?** Every check except parent-link and formal-dependency
validation works on pasted card text.

## Use it in the right place

```
PO drafts card ──▶ [ run this agent ] ──▶ endorse to For Tech Review ──▶ dev
                         ▲
                    here, on your own draft
```

Running it *after* a developer has the card produces a tidier document and the same
number of gaps. The timing is the mechanism.

## The checks

| | Check | Severity | Evidence |
|---|---|---|---|
| G1 | Data contract undefined | BLOCKER | 39 gaps / 29 cards |
| G2 | Cross-surface parity unstated | BLOCKER | 38 gaps / 27 cards |
| G3 | Ambiguous term / quantifier | BLOCKER | 37 gaps / 23 cards |
| G4 | Negative path missing | BLOCKER | 28 gaps / 27 cards |
| G5 | Mechanism prescribed instead of outcome | BLOCKER | 81 cards (27%) |
| G6 | State / lifecycle side-effects undefined | GAP | 24 gaps / 19 cards |
| G7 | Boundary / threshold value missing | GAP | 21 gaps / 16 cards |
| G8 | Dependency outcome unstated | GAP | 23 gaps / 20 cards |
| G9 | Reliability / supportability unstated | GAP | 10 gaps / 9 cards |
| G10 | Idempotency / retry undefined | GAP | 9 gaps / 9 cards |
| G11 | Regression risk unflagged | GAP | 8 gaps / 8 cards |
| G12 | Accessibility unstated | POLISH | 4 gaps / 4 cards |

Seven further checks from a parallel refinement review (Oct 2026):

| | Check | Severity |
|---|---|---|
| G13 | Data provenance unstated | BLOCKER |
| G14 | Fail-open vs fail-safe undecided | BLOCKER |
| G15 | Money formula without a worked example | BLOCKER |
| G16 | Existing records unaddressed | BLOCKER |
| G17 | Cascade on change or delete unstated | GAP |
| G18 | Mockup contradicts the ACs | BLOCKER |
| G19 | Overlap or reversal with another card | GAP |
| G20 | Decision not recorded at Feature level | GAP |

Plus the **silent-decision test**, applied to every AC:

> Is there a call here a developer would have to make on their own?

And one rule that keeps the agent usable: **it must never ask what the card already
answers.** Before raising anything it works a fixed resolution order — this card, then
sibling cards, then the parent Feature, then the Feature's PRD. A question is only a
finding if it survives all four.

Decisions live at **Feature level, in the PRD**. A ruling that stays in a card comment
gets re-asked on the next sibling story — that is check G20.

## Scope guard

**No repo access required.** This is a Product checklist end to end — it asks the PO to
verify no code. Where a claim about the system is involved, the check is that the card
does not make one. Engineering validates engineering claims.

The agent flags only what Product owns. Which component, which library, where a file goes,
how to split cards, branch strategy — engineering's calls, deliberately never flagged.
The test is: *could the PO answer this without a developer?*

An agent that sends POs chasing engineering questions gets ignored within a week.

## Honest limits

- Built from what developers raised on 298 cards. It covers the classes that actually bit,
  not every possible gap. It will not get you to literally zero questions.
- Example card references are from the MallPlus Jira project; swap the
  "Configure for your project" block at the top of the agent for your own.
- Worth re-running the retrospective each quarter to see which checks fired and which
  never did.
