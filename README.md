# bets-lens

A [Claude Code](https://claude.com/claude-code) skill that makes Claude frame substantive work as an explicit **bet** with an honest **1–5 certainty rating** — before building it.

Every roadmap item, feature, and plan is a bet whether or not anyone says so. This skill makes the bet visible:

> "We are building **X** because we believe **Y** will happen."

…and forces an honest answer to *how much do we actually know?*

## The level-of-knowing scale

| Level | Name      | What it means                                                       |
| ----- | --------- | ------------------------------------------------------------------- |
| 1     | Opinion   | We believe this; little or no evidence.                             |
| 2     | Signal    | Anecdotes, support tickets, early patterns — suggestive, not solid. |
| 3     | Evidence  | Meaningful data, research, or repeated behavioral signals.          |
| 4     | Validated | Tested directly; enough confidence to act.                          |
| 5     | Measured  | Shipped and measured; we know what actually happened.               |

The rating measures **evidence**, not confidence. A founder's conviction is a 1. Three users independently asking for the same thing is a 2. When torn between two levels, pick the lower one.

## What Claude does with it

- **States the bet and its rating** before starting any substantive piece of work — one or two sentences, not a form.
- **Challenges level 1–2 bets** by naming the cheapest test that would raise the rating (a prototype, five user conversations, a fake-door test) and offering it as an alternative to building.
- **Never blocks shipping.** The lens informs the decision; you make it. Once you say go, Claude drops the framing and executes.
- **Names the success metric before shipping**, so every bet eventually closes at level 5 — or ends in an honest "the bet failed." Both are wins; the only loss is never finding out.
- **Stays quiet on trivial work.** Typo fixes and small refactors don't get bet-framed.

### Example

> **You:** Let's add a public API so power users can script against us.
>
> **Claude:** The bet: we believe a public API will cause power users to build integrations and deepen retention. Level of knowing: **1 — Opinion** — I haven't seen tickets or user requests cited for this. Cheapest test before committing: interview the five heaviest users about what they'd script, or ship a read-only endpoint for one resource and watch usage. Want to start there, or is this a deliberate flyer?

If you say "build it anyway" — Claude builds it, well, and notes the metric that will tell you whether the bet paid off.

## Install

Clone straight into your Claude Code skills directory:

```bash
git clone https://github.com/ChuckMayo/bets-lens.git ~/.claude/skills/bets-lens
```

That's it. The skill triggers automatically whenever a conversation turns to planning, prioritizing, roadmapping, or scoping new work.

### Optional: always-on nudge

The skill activates when Claude recognizes a planning conversation. For a reminder that rides **every** prompt, install the bundled hook:

```bash
cp ~/.claude/skills/bets-lens/hooks/bets-lens.sh ~/.claude/hooks/bets-lens.sh
chmod +x ~/.claude/hooks/bets-lens.sh
```

Then register it in `~/.claude/settings.json`:

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

The hook injects a one-line reminder on every prompt; the skill carries the full framework. They're complementary.

## Why

Two failure modes kill product teams:

1. **Building on vibes** — committing weeks of effort to something backed by one person's enthusiasm, dressed up as a roadmap item.
2. **Never learning** — shipping things and moving on without ever checking whether the belief behind them was true.

The bets lens is a lightweight discipline against both: make the belief explicit, rate the evidence honestly, prefer the cheapest test over the expensive build when evidence is thin, and always close the loop.

Enthusiasm is not evidence.

## License

[MIT](LICENSE)
