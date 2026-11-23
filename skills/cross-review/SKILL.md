---
name: cross-review
description: Ask OpenAI Codex (a different model than Claude) to review finished work read-only, then verify each finding before applying it. Use when the user says "cross review", "second opinion", "have Codex review this", or after finishing an important deliverable (script, page, report, copy) before closing it.
---

# Cross review — Claude builds, Codex reviews

A second model catches mistakes the first one misses, but it also makes its own. So Codex **only reviews** (read-only sandbox) and Claude **verifies every finding** before touching anything.

## Steps

1. **Define the goal and files.** What was asked, what was delivered, exact paths. If the work isn't finished, finish it first.
2. **Find the Codex CLI.** Use `codex` if it is on PATH. Otherwise look for the binary bundled with the VS Code extension:
   - Windows: `%USERPROFILE%\.vscode\extensions\openai.chatgpt-*\bin\windows-x86_64\codex.exe`
   - macOS/Linux: `~/.vscode/extensions/openai.chatgpt-*/bin/*/codex`
3. **Run the review read-only** from the project root:

   ```bash
   codex exec --skip-git-repo-check -s read-only "<prompt>"
   ```

   Prompt = goal + file paths + criteria (below), ending with:
   "Do not modify any file. Return a numbered list: finding, location, why it matters, proposed fix, severity (high/medium/low). If there are no real issues, say so."
4. **Criteria by type of work:**
   - Copy / pages / scripts for video: follows the project's CLAUDE.md rules, claims are backed, clarity, factual errors.
   - Reports / analysis: unsourced claims, numbers that don't add up, conclusions that exceed the evidence.
   - Code: bugs, edge cases, OS-specific paths, side effects.
5. **Verify each finding** against the file or source. Discard unfounded ones and say why.
6. **Apply only confirmed findings** with minimal edits, then re-validate (build, test, re-read).
7. **Report** in a few lines: what Codex flagged, what was accepted, what was discarded and why.

## Rules

- Codex never publishes, spends or sends anything; neither does this skill.
- Never put keys or tokens in the prompt.
- One round by default; repeat only after substantial changes.
