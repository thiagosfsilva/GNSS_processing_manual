---
name: research-context
description: Technical GNSS processing context, Brazilian geodetic system (SIRGAS2000), and hardware specs
metadata:
  type: project
  author: antigravity
  written: 2026-09-11
---

The project produces an English-language post-processing guide for graduate students working with
GNSS observations in Brazil (e.g. Amazonian floodplains and neotropical wetlands).

Key technical domain constraints:
1. **Reference Frame:** SIRGAS2000 (Sistema de Referência Geocêntrico para as Américas), realizing
   the ITRS in Brazil. The official realization epoch is 2000.4. When comparing field epochs with
   baseline/PPP products, velocity models or epoch discrepancies must be accounted for.
2. **Vertical Datums:** GNSS measures ellipsoidal height ($h$) on the GRS80 ellipsoid. Orthometric
   height ($H$) refers to mean sea level (Imbituba or Santana vertical datum) via geoid
   undulation ($N$): $H = h - N$. In Brazil, $N$ is calculated via MAPGEO2015.
3. **Hardware — Emlid Reach RS2:** Multi-band (L1/L2/L5), multi-constellation (GPS, GLONASS, Galileo,
   BeiDou) RTK/PPK GNSS receiver. The Antenna Reference Point (ARP) is the bottom of the 5/8"
   threaded mount. The Antenna Phase Center (APC) offset is exactly 134 mm (0.134 m) along the
   vertical Z-axis.
4. **Base Station Network — IBGE RBMC:** Rede Brasileira de Monitoramento Contínuo. Distributes
   daily 24-hour RINEX observation logs, compressed using the Hatanaka algorithm (`.crx` / `.yyD`),
   often wrapped in `.gz` or `.zip`. Must be decompressed with `CRX2RNX` before consumption by
   standard GNSS processors.
5. **PPP Service — IBGE PPP:** Free online geodetic service powered by NRCan's CSRS-PPP engine.
   Accepts static dual-frequency GPS/GLONASS RINEX files. Standard recommendation is 30-second
   decimated epochs to avoid transmission bloat and processing errors.

**Why:** Students frequently confuse ellipsoidal and orthometric heights or forget the 134 mm RS2
antenna offset, invalidating vertical datum calculations for hydrological and remote sensing ground
truth.

**How to apply:** Ensure every manual chapter explicitly distinguishes $h$ vs. $H$ and gives
exact ARP/APC offsets and Hatanaka decompression steps.
