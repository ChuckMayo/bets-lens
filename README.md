# bets-lens

## Why

Two failure modes kill product teams:

1. **Building on vibes** — committing weeks of effort to something backed by one person's enthusiasm, dressed up as a roadmap item.
2. **Never learning** — shipping things and moving on without ever checking whether the belief behind them was true.

The bets lens is a lightweight discipline against both: make the belief explicit, rate the evidence honestly, prefer the cheapest test over the expensive build when evidence is thin, and always close the loop.

Enthusiasm is not evidence.

## How it Works

`bets-lens` is a [Claude Code](https://claude.com/claude-code) skill that makes Claude frame substantive work as an explicit **bet** with an honest certainty rating — **Opinion, Signal, Evidence, Validated, or Measured** — before building it.

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

The rating measures **evidence**, not confidence. A founder's conviction is Opinion. Three users independently asking for the same thing is a Signal. When torn between two levels, pick the lower one — and say the name, not the number; the numbers only show the ordering.

## What Claude does with it

- **States the bet and its rating** before starting any substantive piece of work — one or two sentences, not a form.
- **Challenges Opinion- and Signal-level bets** by naming the cheapest test that would raise the rating (a prototype, five user conversations, a fake-door test) and offering it as an alternative to building.
- **Never blocks shipping.** The lens informs the decision; you make it. Once you say go, Claude drops the framing and executes.
- **Names the success metric before shipping**, so every bet eventually closes at Measured — or ends in an honest "the bet failed." Both are wins; the only loss is never finding out.
- **Stays quiet on trivial work.** Typo fixes and small refactors don't get bet-framed.
- **Turns closed bets into receipts.** When a bet closes, Claude drafts a ledger entry (before → after, what it was worth, proof links) — and assembles self-reviews, status updates, and promotion cases from them.

### Example

> **You:** Let's add a public API so power users can script against us.
>
> **Claude:** The bet: we believe a public API will cause power users to build integrations and deepen retention. Level of knowing: **Opinion** — I haven't seen tickets or user requests cited for this. Cheapest test before committing: interview the five heaviest users about what they'd script, or ship a read-only endpoint for one resource and watch usage. Want to start there, or is this a deliberate flyer?

If you say "build it anyway" — Claude builds it, well, and notes the metric that will tell you whether the bet paid off.

## Receipts: when you find out, write it down

The skill asks: *what are you betting on, and how will you know it worked?* Receipts add one move: **when you find out, write it down — and show people.** Promotions and renewals are decided in rooms you're not in, from written evidence. People with receipts don't have to argue.

The whole mechanic:

1. Before you start, write down today's number.
2. When you finish, write down the new number.
3. That before→after line is your receipt. Keep them all in one doc. Share a few now and then. Never exaggerate.

When you share one, say it in one sentence, in terms the reader cares about: *"I did X, which moved Y from A to B, which mattered because Z."*

The fine print (tested by running a real month of work through the filter — 233 merged PRs distilled to ~20 receipts):

- Most work won't produce a receipt. Normal — a few good ones a quarter is plenty.
- Tests, refactors, and tooling are the proof line of a receipt, not the receipt.
- "Merged" is not a receipt. Live and verified is.
- Some of your best receipts already exist — work you finished but never measured. Go read the number.
- Helping someone else score counts. Claim the assist, not their number.
- Failed bets get receipts too. Never round up.
- Put a read-by date on every open bet (when will the number be ripe?), sweep the overdue ones each time you write your weekly note, and celebrate the wins out loud where the team lives.

Ask Claude for a self-review, brag doc, or promo packet and it assembles them from your receipts. Ask it for an **open-loops sweep** and it finds the receipts you already earned but never collected — and stays quiet about the ones whose numbers aren't ripe yet.

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

## License

[MIT](LICENSE)
