---
name: session-state
description: Where GNSS Post-Processing Manual stands and the immediate next action
metadata:
  type: project
---

**Last updated:** 2026-09-27 by antigravity, after creating the public GitHub repository and deploying to GitHub Pages.

## Where things stand

- **Phase 1 (Scaffolding & Governance):** COMPLETE (verified in commit `bfee83a`).
  - `git init`, `.gitignore`, `AGENTS.md`, `CLAUDE.md`, `.agents/rules/antigravity.md`, `PLAN.md`, `_quarto.yml`, `README.md`.
- **Phase 2 (Foundations & IBGE RBMC Workflow):** COMPLETE (verified in commit `bfee83a`).
  - `sections/01_foundations.qmd`: Concepts, PPK vs PPP, SIRGAS2000 epoch 2000.4, Ellipsoidal ($h$) vs Orthometric ($H$) height, MAPGEO2015, Reach RS2 antenna geometry (ARP vs APC 0.134 m).
  - `sections/02_ibge_rbmc_download.qmd`: Finding nearest RBMC station, GeoFTP directory structure, file naming conventions, site logs, Hatanaka decompression with `CRX2RNX.exe` and PowerShell batch script.
- **Phase 3 (Emlid Studio PPK):** COMPLETE (verified in commit `bfee83a`).
  - `sections/03_emlid_studio_ppk.qmd`: GUI walkthrough, Reach RS2 antenna offsets, base position manual override with official IBGE coordinates, advanced processing filters, Fix vs Float QC, local image assets in `assets/images/`.
- **Phase 4 (RTKlib Decimation & IBGE PPP):** COMPLETE (verified in commit `bfee83a`).
  - `sections/04_rtklib_rinex_prep.qmd`: 30-second decimation rationale, RTKCONV GUI walkthrough, RINEX 2.11 formatting, header editing, `convbin` CLI alternative.
  - `sections/05_ibge_ppp_submission.qmd`: IBGE PPP online form parameters, antenna model selection (`EML_REACH_RS2` vs `ADVNULLANTENNA`), IGS ephemeris tiers (Final vs Rapid), PDF report interpretation (coordinates, standard deviations, orthometric elevation).
  - `sections/06_troubleshooting_faqs.qmd`: Float trap diagnostics, RBMC ingestion errors, PPP rejection causes, antenna height offset summary table, field protocol checklist.
- **Phase 5 (Master Document & Compilation):** COMPLETE (verified with dual HTML & PDF compilation).
  - `index.qmd`: Master document assembling all sections without local format overrides.
  - `_quarto.yml`: Configured with explicit `render: [index.qmd]`, dual `html` and `pdf` formats.
  - `GNSS_processing_manual.Rproj`: RStudio project root configured.
- **Phase 6 (GitHub Deployment & CI/CD):** COMPLETE.
  - Public GitHub repository: [thiagosfsilva/GNSS_processing_manual](https://github.com/thiagosfsilva/GNSS_processing_manual).
  - Default branch: `main`.
  - Live GitHub Pages site: [https://thiagosfsilva.github.io/GNSS_processing_manual/](https://thiagosfsilva.github.io/GNSS_processing_manual/) deployed via `quarto publish gh-pages`.
  - Automated CI/CD: `.github/workflows/quarto-publish.yml` triggers automated render and deploy on pushes to `main`.

## Immediate next action

Manual is live. Periodic maintenance or content updates as research workflows evolve.

