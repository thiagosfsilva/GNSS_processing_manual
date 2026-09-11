@AGENTS.md

# Claude Code — harness-specific instructions

Everything about the *project* lives in `AGENTS.md`, imported above. This file holds only what
stops being true when a different tool opens the repository. **Never put project knowledge here.**

## Tools and shell

- Windows locally: PowerShell 7 is the primary shell.
- For file inspection, prefer dedicated tools (Glob, Grep, Read) over shell commands.
- Never pass multi-line text directly as a shell argument — write to a file first.

## Scratchpad

Temporary files and test conversions go in `scratch/` or `tmp/` (gitignored).

## Memory

- Every memory write must land in the repository's `memory/` folder and be committed.
- Claude Code is a scoped contributor: add new fact files and append your own dated entry to
  `memory/session_state.md`. Do not consolidate or prune entries created by the lead tool.
