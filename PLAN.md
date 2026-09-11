# PLAN — GNSS Post-Processing Manual

Written 2026-09-11. **Authoritative** for the decisions taken and the phases outstanding. Cite it
by section number. Nothing in this document is executed until the user says go.

## 1. What we are building and why

This project produces a comprehensive, pedagogical manual in English on post-processing GNSS
acquisitions, aimed at a PhD student who has not processed GNSS observations before. The manual
serves as a practical lab guide, bridging the gap between field data acquisition and rigorous,
publishable geodetic coordinates.

The guide covers four interconnected workflows: (1) downloading reference station data from the
Brazilian IBGE RBMC (Rede Brasileira de Monitoramento Contínuo) network, including Hatanaka
decompression; (2) post-processing kinematic/static (PPK) baselines in Emlid Studio using an
Emlid Reach RS2 receiver and an IBGE RBMC base station; (3) preparing raw GNSS RINEX logs using
RTKlib (RTKCONV GUI) for IBGE PPP processing (30-second epoch decimation and format conversion);
and (4) submitting RINEX files to the online IBGE PPP service and interpreting the resulting
SIRGAS2000 coordinates, formal standard deviations, and ellipsoidal vs. orthometric heights.
The project is built as a Quarto document (`project: type: default`) with Windows-first GUI
walkthroughs, native Mermaid diagrams, and authentic reference screenshots.

## 2. Locked decisions

| # | Decision | Why | Date |
|---|---|---|---|
| 2.1 | Quarto Document (`project: type: default`) with modular child chapters in `sections/` compiled into `index.qmd`. | Enables clean modular authoring while rendering to a unified, polished publication document (HTML/PDF). | 2026-09-11 |
| 2.2 | Windows-first and GUI-driven. | Focuses on Windows GUI workflows (Emlid Studio Windows, RTKCONV GUI, IBGE web portals) with copy-pasteable CLI commands where useful (`convbin`, `crx2rnx`). | 2026-09-11 |
| 2.3 | Native Mermaid diagrams + authentic UI reference images in `assets/images/`. | Zero AI-hallucinated imagery; clear structural diagrams rendered natively, backed by real software screenshots. | 2026-09-11 |
| 2.4 | Include Hatanaka decompression (CRX2RNX) and GFZRNX alongside RTKlib. | IBGE RBMC distributes daily files in compact Hatanaka format (`.crx` / `.yyD` / `.gz`); students must decompress them to avoid ingestion errors. | 2026-09-11 |
| 2.5 | Practical conceptual callout boxes alongside procedural steps. | Explains key geodesy concepts (SIRGAS2000 vs WGS84, ellipsoidal vs orthometric height via MAPGEO, Fix vs Float, why 30s decimation is standard) alongside button clicks. | 2026-09-11 |
| 2.6 | Generic station & session identifiers (`BASE00`, generic coordinates). | Clean, reproducible examples that do not depend on ephemeral single-station availability. | 2026-09-11 |
| 2.7 | Lean Git tracking policy (Zone A/B/C). | Only source `.qmd`, Mermaid diagrams, configs, and lightweight UI images are tracked. Sample raw GNSS logs (`.ubx`, `.obs`, `.rnx`, `.crx`, `.zip`) are ignored via `.gitignore`. | 2026-09-11 |
| 2.8 | Antigravity leads; Claude Code & Codex in play. | Canonical `AGENTS.md` at repo root; tool harness files `CLAUDE.md` and `.agents/rules/antigravity.md`; in-repo `memory/`. | 2026-09-11 |

## 3. Target structure

```
GNSS_processing_manual/
├── .agents/
│   └── rules/
│       └── antigravity.md         # Antigravity harness file
├── assets/
│   └── images/                    # Authentic reference UI screenshots & graphics
├── memory/
│   ├── MEMORY.md                  # In-repo memory index
│   ├── session_state.md           # Session continuity & current step
│   └── research-context.md        # Technical GNSS / Brazilian geodesy context
├── sections/
│   ├── 01_foundations.qmd         # Conceptual primer: PPK vs PPP, datums, heights
│   ├── 02_ibge_rbmc_download.qmd  # Step-by-step RBMC download, site logs, CRX2RNX
│   ├── 03_emlid_studio_ppk.qmd    # Emlid Studio PPK, RS2 antenna offsets, Fix/Float QC
│   ├── 04_rtklib_rinex_prep.qmd   # RTKCONV GUI 30s decimation, header & antenna setup
│   ├── 05_ibge_ppp_submission.qmd # IBGE PPP portal submission & PDF report interpretation
│   └── 06_troubleshooting_faqs.qmd# Student FAQs, common errors, and best practices
├── .gitignore                     # Ignores raw GNSS logs, cache, and build outputs
├── _quarto.yml                    # Quarto project configuration
├── AGENTS.md                      # Canonical project governance and stack rules
├── CLAUDE.md                      # Claude Code harness file
├── index.qmd                      # Master document assembling all sections
└── PLAN.md                        # Authoritative project plan
```

## 4. Phases

| Phase | Produces | Gate |
|---|---|---|
| 1 | Repository skeleton & governance: `git init`, `.gitignore`, `AGENTS.md`, `CLAUDE.md`, `.agents/rules/antigravity.md`, `memory/`, `_quarto.yml`, `index.qmd` scaffold. | Clean git tree; no untracked raw data; harness files and memory files present without drift. |
| 2 | Foundations & IBGE RBMC workflow: `sections/01_foundations.qmd` and `sections/02_ibge_rbmc_download.qmd`. | Clear conceptual callouts (SIRGAS2000, MAPGEO, PPK vs PPP); step-by-step RBMC download and Hatanaka decompression steps verified. |
| 3 | Emlid Studio PPK workflow: `sections/03_emlid_studio_ppk.qmd`. | Reach RS2 antenna offsets (ARP vs APC 0.134 m) documented; GUI navigation verified; Fix/Float QC metrics defined. |
| 4 | RTKlib 30s decimation & IBGE PPP submission: `sections/04_rtklib_rinex_prep.qmd`, `sections/05_ibge_ppp_submission.qmd`, `sections/06_troubleshooting_faqs.qmd`. | RTKCONV GUI decimation procedure clear; IBGE PPP form parameters and report interpretation (standard deviations, SIRGAS2000 epoch, heights) fully explained. |
| 5 | Review, rendering check, and house audit: asset assembly, Quarto render verification, pass over `references/audit.md`. | Quarto document renders cleanly to HTML/PDF; all Mermaid blocks valid; no placeholders surviving; audit findings reported. |

## 5. Verification

- **Quarto compilation:** Verify that `quarto render` compiles `index.qmd` and all child documents in `sections/` without syntax or inclusion errors.
- **Mermaid syntax:** All Mermaid diagrams pass Quarto rendering without parsing failures.
- **Link and path integrity:** All section cross-references and asset paths resolve cleanly.
- **Self-Audit:** Review against `references/audit.md` before reporting completion.

## 6. Open decisions

| # | Question | Default if unanswered | Settled by |
|---|---|---|---|
| 6.1 | PDF rendering engine for Quarto (Typst vs. LaTeX/TinyTeX). | Default to HTML render as primary; PDF enabled via Typst if available, or HTML exportable to PDF. | Checking local environment tools. |
| 6.2 | Antenna descriptor in RINEX header for IBGE PPP. | Default to specifying `EML_REACH_RS2 NONE` when recognized by the geodetic service, with instructions on using `ADVNULLANTENNA` with exact measured height to ARP if custom antenna phase center models are unsupported. | Documenting both standard geodetic and fallback practices in Section 4. |

## 7. Out of scope

- Automated batch processing pipelines / automated scraping scripts (deferred to future work if needed).
- Compiling RTKlib C source code from scratch (manual uses official pre-compiled Windows binaries).
- Linux / macOS command-line setup (focus is strictly Windows-first and GUI-driven).
