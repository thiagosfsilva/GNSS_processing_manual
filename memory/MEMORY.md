# Project memory index

One fact per file. Read this index first, then `session_state.md`, then load individual files
only as the task needs them — never the folder wholesale.

This folder lives in the repo, not in any one tool's private store, so every tool can read it
and it survives a new machine. Nothing of record belongs in `~/.claude/projects/<slug>/memory/`
or `~/.gemini/antigravity/knowledge/`.
Every tool that works on this project also writes here — whoever did the work records it, in
the same session, dated and attributed, as a **new file** rather than an edit to someone
else's. Antigravity owns coherence: consolidating, pruning, and keeping this index in step
with the folder (see the write-scope table in `AGENTS.md`).

Every file is a snapshot of what was true when written. If one names a file, function or flag,
verify it still exists before acting on it. Memory is convenient context, not the source of
truth: code, the governance docs and git history outrank it.

- [Session state](session_state.md) — where the project stands and the immediate next action
- [Research context](research-context.md) — GNSS processing domain, Brazilian geodetic datum, and field constraints
