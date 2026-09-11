# GNSS Post-Processing Manual: Field-to-Coordinates Guide for Researchers

A comprehensive, pedagogical manual in English on post-processing GNSS acquisitions, designed specifically for graduate students, postdocs, and environmental researchers in ecology and remote sensing who have not performed geodetic post-processing before.

The manual covers four interconnected workflows:
1. **Downloading reference station data from the Brazilian IBGE RBMC network**, including site log interpretation and Hatanaka decompression with `CRX2RNX`.
2. **Post-processing kinematic and static baselines (PPK) in Emlid Studio** using raw logs from the Emlid Reach RS2 receiver and RBMC reference stations.
3. **Decimating and formatting RINEX observation logs to 30-second intervals in RTKlib (RTKCONV GUI / `convbin`)** for static geodetic processing.
4. **Submitting observation logs to the IBGE PPP (Precise Point Positioning) service** and decoding output PDF reports (SIRGAS2000 epoch 2000.4 coordinates, formal standard deviations, and MAPGEO2015 orthometric elevations).

---

## Document Structure

The manual is authored in Quarto (`.qmd`) with native Mermaid workflow diagrams and official software UI reference figures:

```
GNSS_processing_manual/
├── _quarto.yml                    # Quarto document configuration
├── index.qmd                      # Master document assembling all chapters
├── sections/
│   ├── 01_foundations.qmd         # Conceptual primer: PPK vs PPP, SIRGAS2000, datums, heights
│   ├── 02_ibge_rbmc_download.qmd  # Downloading RBMC data, station selection, CRX2RNX
│   ├── 03_emlid_studio_ppk.qmd    # Emlid Studio PPK, RS2 antenna offsets, Fix/Float QC
│   ├── 04_rtklib_rinex_prep.qmd   # RTKCONV GUI 30s decimation, header & antenna setup
│   ├── 05_ibge_ppp_submission.qmd # IBGE PPP portal submission & PDF report interpretation
│   └── 06_troubleshooting_faqs.qmd# Student FAQs, common errors, and field checklist
├── assets/
│   └── images/                    # Local reference figures and screenshots
└── PLAN.md                        # Project plan and locked decisions
```

---

## Software and Utilities Covered

* **Emlid Studio:** Free multi-platform post-processing software ([Emlid Studio](https://emlid.com/emlid-studio/)).
* **RTKLIB (RTKCONV / convbin):** Open-source GNSS analysis and format conversion suite ([RTKLIB releases](https://github.com/rtklibexplorer/RTKLIB/releases)).
* **CRX2RNX:** Official Hatanaka Compact RINEX decompression utility ([IGS Tools](https://gage.earthscope.org/data/gnss/hatanaka.html)).
* **IBGE PPP Web Portal:** Online geodetic PPP service powered by NRCan CSRS-PPP ([IBGE PPP Portal](https://www.ibge.gov.br/geociencias/informacoes-sobre-posicionamento-geodesico/servicos-online-para-posicionamento/16281-servico-online-para-posicionamento-por-ponto-preciso.html)).

---

## Rendering the Manual

To render the complete manual to HTML or PDF using [Quarto](https://quarto.org/):

```powershell
# Render HTML document (output to _site/index.html)
quarto render index.qmd --to html

# Render PDF document (requires LaTeX or Typst)
quarto render index.qmd --to pdf
```

---

## Data and Git Tracking Policy

* **Tracked (Zone A):** Quarto source files (`index.qmd`, `sections/*.qmd`), Mermaid diagram blocks, configuration files, and documentation.
* **Untracked (Zone C):** Raw GNSS observation files (`*.ubx`, `*.obs`, `*.rnx`, `*.crx`, `*.zip`) are ignored via `.gitignore` and must never be committed to Git history.
