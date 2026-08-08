@AGENTS.md

## Claude Code

- Permission rules for this repository go in `.claude/settings.local.json`
  (git-ignored).
- The auto-mode classifier blocks commands that read stored credentials (Hex
  OAuth tokens, CLI auth files) and commands that change security settings, even
  when chat gives permission. Expect these steps to fall back to the user.
- This repository is empty on purpose. Read the "First questions" section of
  AGENTS.md before you write code. Every one of those questions is open, and
  answering one by writing code is the wrong order.
