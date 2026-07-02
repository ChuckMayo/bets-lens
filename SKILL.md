---
name: bets-lens
description: >-
  Frame work as explicit bets with an honest 1-5 certainty rating (the
  level-of-knowing scale) before building. Use this whenever the user is
  planning, prioritizing, roadmapping, scoping a feature, writing a spec or
  PRD, deciding what to build next, reviewing a plan, or kicking off any
  substantive new work — even if they never say the word "bet." Also use it
  when the user asks "what's the bet," "how sure are we," "what's our level
  of knowing," "should we build X," or asks you to challenge or pressure-test
  an idea, and when closing out shipped work ("did it work?").
---

# Bets Lens

A discipline for keeping ambition honest. Every piece of substantive work is a
bet, whether or not anyone says so — this skill makes the bet explicit, rates
how much we actually know, and closes the loop after shipping.

The point is not paperwork. It is to stop two failure modes:

1. **Building on vibes** — committing serious effort to something backed by
   one person's enthusiasm, dressed up as a roadmap item.
2. **Never learning** — shipping things and moving on without ever checking
   whether the belief behind them was true.

## The bet statement

Before building, state the bet in one sentence:

> "We are building **X** because we believe **Y** will happen."

If you cannot fill in Y, that is the finding — say so. Work with no
articulable belief behind it is either a chore (fine, just call it that) or a
bet nobody has thought through (not fine).

## The level-of-knowing scale

Rate every bet 1-5. The rating measures **evidence**, not confidence or
excitement:

| Level | Name      | What it means                                                        |
| ----- | --------- | -------------------------------------------------------------------- |
| 1     | Opinion   | We believe this; little or no evidence.                              |
| 2     | Signal    | Anecdotes, support tickets, early patterns — suggestive, not solid.  |
| 3     | Evidence  | Meaningful data, research, or repeated behavioral signals.           |
| 4     | Validated | Tested directly; enough confidence to act.                           |
| 5     | Measured  | Shipped and measured; we know what actually happened.                |

Ratings are honest. Enthusiasm is not evidence. A founder's conviction is a 1.
Three users independently asking for the same thing is a 2. A well-run user
test is a 4. If you are torn between two levels, pick the lower one.

## The discipline

**Commitments need level 3+.** Committing real effort to a level 1-2 bet
requires either an explicit, stated reason ("this is cheap and reversible,"
"we're deliberately taking a flyer") or the cheapest possible test that would
raise it to 3 — a prototype, five user conversations, a fake-door test.
Propose that test before proposing the build.

**Define the success metric before shipping.** Every bet names, up front, how
we will know whether Y happened. This is what lets a shipped bet close the
loop at level 5 — or end in an honest "the bet failed." Both outcomes are
wins; the only loss is never finding out.

**Horizons have jobs.** Current work is for execution and learning. The next
commitment is for rated bets. Anything further out is shaping — and walking
away from a shaped idea is a legitimate, cheap outcome, not a failure.

## How to apply this in conversation

- When the user kicks off substantive new work, state the implied bet and
  your honest level-of-knowing rating **before** building. One or two
  sentences — this is a lens, not a form.
- **Challenge level 1-2 bets.** Name the cheapest test that would move the
  rating up, and offer it as an alternative to building. Be direct but brief.
- **Never block shipping when the user says go.** The lens informs the
  decision; the user makes it. Once they decide, drop the framing and
  execute well. Do not re-litigate.
- When work ships, remind them of the metric: what would we look at, and
  when, to close this bet at level 5?
- Skip the framing entirely for trivial work (typo fixes, small refactors,
  answering questions) — and skip it **silently**. Don't announce that the
  lens doesn't apply; just answer. Applying bet discipline to a one-line fix
  is noise and erodes trust in the lens, and so does narrating its absence.

## Example

**User:** "Let's add a public API so power users can script against us."

**Applying the lens:**

> The bet: we believe a public API will cause power users to build
> integrations and deepen retention. Level of knowing: **1 — Opinion**. I
> haven't seen tickets or user requests cited for this. Cheapest test before
> committing: interview the five heaviest users about what they'd script, or
> ship a read-only endpoint for one resource and watch usage. Want to start
> there, or is this a deliberate flyer?

If the user says "I hear you, build it anyway" — build it, well, and note the
success metric (e.g., "N distinct API consumers within a month of launch").

## Optional: always-on nudge (Claude Code hook)

The skill triggers when conversation touches planning. For an always-on
version that rides every prompt, install the bundled UserPromptSubmit hook:

1. Copy `hooks/bets-lens.sh` to `~/.claude/hooks/bets-lens.sh` and make it
   executable (`chmod +x`).
2. Register it in `~/.claude/settings.json`:

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [{ "type": "command", "command": "~/.claude/hooks/bets-lens.sh" }]
      }
    ]
  }
}
```

The hook injects a one-line reminder on every prompt; the skill body carries
the full framework. They are complementary — the hook keeps the lens present,
the skill explains how to use it.
