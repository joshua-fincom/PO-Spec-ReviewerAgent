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
| Cards asserting a reuse/existence claim the dev had to disprove | **27%** |

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
| G5 | Code-reality claim unverified | BLOCKER | 81 cards (27%) |
| G6 | State / lifecycle side-effects undefined | GAP | 24 gaps / 19 cards |
| G7 | Boundary / threshold value missing | GAP | 21 gaps / 16 cards |
| G8 | Integration assumption unverified | GAP | 23 gaps / 20 cards |
| G9 | Reliability / supportability unstated | GAP | 10 gaps / 9 cards |
| G10 | Idempotency / retry undefined | GAP | 9 gaps / 9 cards |
| G11 | Regression risk unflagged | GAP | 8 gaps / 8 cards |
| G12 | Accessibility unstated | POLISH | 4 gaps / 4 cards |

Plus the **silent-decision test**, applied to every AC:

> Is there a call here a developer would have to make on their own?

## Scope guard

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
