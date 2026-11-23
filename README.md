# claude-cross-review

A [Claude Code](https://claude.com/claude-code) skill that gets a **second opinion from a different model**: Claude finishes the work, OpenAI Codex reviews it in a read-only sandbox, and Claude verifies every finding before applying it.

Why: a reviewer from another model family catches blind spots the author model shares with itself — but reviewers are wrong too, so nothing is applied without verification.

## Install

Copy `skills/cross-review/` into your project's `.claude/skills/` (or `~/.claude/skills/` for all projects).

Requires the Codex CLI (`codex`) or the OpenAI VS Code extension, which bundles it.

## Use

In Claude Code: "cross review this", "have Codex review it", or `/cross-review`.

## License

MIT
