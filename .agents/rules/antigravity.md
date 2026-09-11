# Antigravity — harness-specific instructions

Everything about the *project* lives in `AGENTS.md` at the repository root, which Antigravity
parses directly — read it first. This file holds only what stops being true when a different tool
opens the repository. **Never put project knowledge here.**

Do not create a workspace-root `GEMINI.md`. This file is the one place.

## Artifacts

Artifacts — implementation plans, walkthroughs — are agent working output, not project record.
They are gitignored.
- Never cite an Artifact path as the record of a decision.
- Promoted deliverables belong in `sections/`, `docs/`, or project root files.

## Subagents

- Prefer `define_subagent` over stored definitions.
- Default to `model: inherit`.
- Never create an `.agents/agents/` file unasked.

## Memory

- Every memory write must land in the repository's `memory/` folder and be committed.
- Antigravity is the lead tool: it owns coherence, consolidating, pruning, and keeping
  `MEMORY.md` in step.
- Update `memory/session_state.md` at the end of every session.
