# GNSS Post-Processing Manual — project instructions

Canonical, agent-neutral instructions. Codex and Antigravity read this file directly; Claude
Code reads it through the `@AGENTS.md` import at the top of `CLAUDE.md`. Harness-specific detail
(tool names, shell wrappers, session bookkeeping) belongs in that tool's own harness file —
`CLAUDE.md`, or `.agents/rules/antigravity.md` — never here; project knowledge belongs here,
never only in a harness file. **Two copies of the same instructions always drift.**

## Working together

This is about collaboration, not harness permissions. Permission modes decide what a tool *may
execute*; this decides what it *should do*. **The user stays in control at all times.**

**The working cycle:** the user says what they want → you ask until you both agree → they say
**go** → you execute that scope autonomously → you stop at its edge and report.

- **Before the go, ask; do not build.** While the shape of the work is unsettled, interact
  frequently: show the step, say what you would do next, wait.
- **After the go, work autonomously inside the agreed scope** — code, tests, docs, ordinary
  implementation choices. Do not check in step by step; do not ask permission for ordinary
  edits.
- **Stop at the edge of the scope.** Anything the go did not cover is a new cycle: say what you
  found, and ask.
- **A question gets an answer, not an implementation.** A question is not a go.
- **Troubleshooting carries its own autonomy** — a diagnosis follows the thread wherever it
  leads. Fixing what you find is a separate decision.
- **Never guess. Ask.** If two readings of the request lead to different work, ask which.
- **Do not be eager.** After a change, stop once it is done and correctly described. Never
  auto-launch the app or server, never auto-run verification scripts, never chain into "let me
  also check X". Offer verification rather than performing it.

**Corrections:**

- **Correct only what was corrected.** A correction applies to the thing corrected. Do not
  generalise it into a principle, and do not apply it to adjacent text that was not mentioned,
  unless told to. If it seems to imply a wider change, say so and ask.
- **Never resolve a conflict yourself.** When a new instruction appears to contradict standing
  text, stop. Name both, say which you think should win and why, and wait. Do not pick.
- **Land where the correction points, not past it.** The correction marks a position, not a
  direction of travel.
- **Do not build a replacement for something being removed** unless asked.

## What this project is

A pedagogical, publication-standard manual in English explaining how to post-process GNSS
acquisitions, written specifically for PhD students and researchers in ecology, environmental
science, and remote sensing who have not previously conducted geodetic post-processing.

The manual provides rigorous, step-by-step instructions across four core workflows:
1. Downloading and decompressing reference station data from the Brazilian IBGE RBMC (Rede
   Brasileira de Monitoramento Contínuo) network.
2. Post-processing kinematic/static (PPK) baseline solutions using Emlid Reach RS2 receiver logs
   and RBMC reference stations in Emlid Studio.
3. Preparing and decimating raw GNSS RINEX logs (to 30-second intervals) and converting formats
   using RTKlib (RTKCONV GUI / `convbin`).
4. Submitting RINEX files to the online IBGE PPP (Posicionamento por Ponto Preciso) service and
   interpreting resulting coordinates, standard deviations, and vertical datums (SIRGAS2000
   and MAPGEO orthometric heights).

## Start of every session

1. Read `memory/MEMORY.md` — the index of project memory.
2. Read `memory/session_state.md` — what was done last, and the immediate next action.
3. Read further memory files only as the task needs them. Do not load the folder wholesale.

**Memory conventions.** One fact per file. YAML frontmatter carries `name`, `description`,
`metadata.type` (`user` | `feedback` | `project` | `reference`), `author`, and `written`.
`[[wikilinks]]` in the body reference another file by its `name:` slug. `memory/archive/` holds
dated snapshots kept for provenance — they are NOT current state and must never be read as live
context.

Every memory file is a snapshot of what was true when written. If one names a file, function
or flag, verify it still exists before acting on it. Memory is convenient context, not the
source of truth: code, the governance docs and git history outrank it.

## Software stack and authoring format

**Main stack: Quarto Document (`_quarto.yml`, `.qmd`).**
- **Document format:** Single comprehensive document composed of modular child chapters
  located in `sections/` and assembled via `index.qmd`.
- **Target OS & shell:** Windows locally using native Windows tooling and **PowerShell 7**.
- **Visuals:** Native Mermaid diagrams within Quarto code blocks (````{mermaid}````) for
  architectural flowcharts, signal processing sequences, and antenna offset geometries. Local
  screenshots and schematics stored under `assets/images/`.
- **Tone:** Methodological clarity suited for graduate students; conceptual callout boxes
  explaining geodesy concepts (SIRGAS2000 vs. WGS84, ellipsoidal vs. orthometric height via
  MAPGEO, Fix vs. Float solutions, 30s decimation rationale) paired with step-by-step GUI
  walkthroughs.

## Invariants

- **Windows GUI first:** Instructions must walk through Windows GUI applications (Emlid Studio
  for Windows, RTKCONV GUI, IBGE web portals) with copy-pasteable CLI commands (`convbin`,
  `crx2rnx`) as supplemental alternatives.
- **Decompression requirement:** Always explain and account for Hatanaka compression (`.crx` /
  `.yyD` / `.gz`) when working with IBGE RBMC data, as unprocessed Hatanaka files fail to ingest
  in standard GNSS software.
- **Antenna offset accuracy:** The antenna reference point (ARP) to antenna phase center (APC)
  geometry of the Emlid Reach RS2 (0.134 m offset from the bottom mount 5/8" thread) must be
  explicitly maintained and explained.
- **No AI-generated hallucinations:** Diagrams are rendered in native Mermaid; images are
  authentic reference screenshots from software documentation and official portals.

## Data zones

`PLAN.md` §3 maps the folder structure. **Lean Git tracking** governs:
- **Zone A — tracked:** Source text (`.qmd`), diagrams (Mermaid code), configuration files
  (`_quarto.yml`), governance (`AGENTS.md`, `PLAN.md`), and lightweight UI reference images in
  `assets/images/`.
- **Zone B — derived/compiled:** HTML or PDF render outputs (`_site/`, `index.html`) if built.
- **Zone C — untracked:** Raw GNSS observation files (`*.ubx`, `*.obs`, `*.rnx`, `*.crx`,
  `*.zip`, RINEX daily files). These are ignored in `.gitignore` and must never be committed.

## Tooling and write scope

**Antigravity leads this project.** It is the UI this project is driven from, and it owns
project state — so there is exactly one narrative of where things stand. It owns orchestration,
subagents, structure, the plan, and the governance docs.

**Claude Code and Codex contribute in scope:** single-section authoring and technical review
inside the established outline. A change that would alter the project structure or locked
decisions stops and comes back to the lead.

| Surface | Antigravity | Claude Code | Codex |
|---|---|---|---|
| Sections (`sections/*.qmd`), `index.qmd`, `_quarto.yml`, `README.md` | write | write | write |
| `memory/` fact files, own `session_state.md` entries | write | write | write |
| `memory/` structure: consolidating, pruning, editing others' entries | write | no | no |
| Governance docs (`AGENTS.md`, `PLAN.md`) | write | read only; propose in chat | read only; propose in chat |
| Own harness file (`.agents/rules/antigravity.md`, `CLAUDE.md`) | write | propose in chat | read only |

Every tool writes memory. Whoever does the work records it, dated and attributed. Commit before
switching tools, and never leave a half-finished edit for another to find.

## Documentation policy

- **Exactly one `README.md` — the one at the repo root.**
- Keep it in sync with reality in the same commit as structural changes.
- Student-facing manual content lives in `sections/*.qmd` and `index.qmd`.

## Approval boundaries

Stop and get explicit approval before:
- Committing any binary file over 5 MB.
- Altering the locked decisions recorded in `PLAN.md` §2.
- Running long-running external download loops or scraping scripts.
