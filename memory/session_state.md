---
name: session-state
description: Where GNSS Post-Processing Manual stands and the immediate next action
metadata:
  type: project
---

**Last updated:** 2026-09-11 by antigravity, after completing all drafting, structuring, and self-audit phases.

## Where things stand

- **Phase 1 (Scaffolding & Governance):** COMPLETE.
  - `git init`, `.gitignore`, `AGENTS.md`, `CLAUDE.md`, `.agents/rules/antigravity.md`, `PLAN.md`, `_quarto.yml`, `README.md`.
- **Phase 2 (Foundations & IBGE RBMC Workflow):** COMPLETE.
  - `sections/01_foundations.qmd`: Concepts, PPK vs PPP, SIRGAS2000 epoch 2000.4, Ellipsoidal ($h$) vs Orthometric ($H$) height, MAPGEO2015, Reach RS2 antenna geometry (ARP vs APC 0.134 m).
  - `sections/02_ibge_rbmc_download.qmd`: Finding nearest RBMC station, GeoFTP directory structure, file naming conventions, site logs, Hatanaka decompression with `CRX2RNX.exe` and PowerShell batch script.
- **Phase 3 (Emlid Studio PPK):** COMPLETE.
  - `sections/03_emlid_studio_ppk.qmd`: GUI walkthrough, Reach RS2 antenna offsets, base position manual override with official IBGE coordinates, advanced processing filters, Fix vs Float QC.
- **Phase 4 (RTKlib Decimation & IBGE PPP):** COMPLETE.
  - `sections/04_rtklib_rinex_prep.qmd`: 30-second decimation rationale, RTKCONV GUI walkthrough, RINEX 2.11 formatting, header editing, `convbin` CLI alternative.
  - `sections/05_ibge_ppp_submission.qmd`: IBGE PPP online form parameters, antenna model selection (`EML_REACH_RS2` vs `ADVNULLANTENNA`), IGS ephemeris tiers (Final vs Rapid), PDF report interpretation (coordinates, standard deviations, orthometric elevation).
  - `sections/06_troubleshooting_faqs.qmd`: Float trap diagnostics, RBMC ingestion errors, PPP rejection causes, antenna height offset summary table, field protocol checklist.
- **Phase 5 (Master Document & Self-Audit):** COMPLETE.
  - `index.qmd`: Master document incorporating all sections.
  - Self-audit against `references/audit.md` completed with zero drift findings.

## Immediate next action

Present completed manual walkthrough to Thiago for review.

## Next, in order

1. User review of the manual content and pedagogical flow.
2. Initial Git commit of the scaffolded repository (Zone A assets).
3. Optional Quarto HTML / PDF compilation verification if Quarto environment is configured.
