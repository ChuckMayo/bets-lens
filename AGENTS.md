# Repository Guidelines

This repo is a single AI skill shared by Codex and Claude Code.

## Shape

- Keep `SKILL.md` at the repo root. Codex users may install this repo as the root skill path (`.`) with the skill name `bets-lens`.
- Keep trigger-critical wording in the `description` frontmatter of `SKILL.md`; README prose does not affect automatic invocation.
- Keep `agents/openai.yaml` aligned with `SKILL.md` whenever the skill purpose or default prompt changes.
- Treat `hooks/bets-lens.sh` as Claude Code-specific unless Codex gains compatible hook support.

## Validation

After changing `SKILL.md` or `agents/openai.yaml`, run:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
```

If `python3` lacks dependencies locally, use the Codex-bundled runtime or pass `--name bets-lens` to helper scripts that otherwise need to parse YAML.

## Style

- Keep the skill concise and agent-facing. Prefer useful operating rules over explanatory essays.
- Preserve the level names exactly: `Opinion`, `Signal`, `Evidence`, `Validated`, and `Measured`.
- Preserve the principle: enthusiasm is not evidence.
