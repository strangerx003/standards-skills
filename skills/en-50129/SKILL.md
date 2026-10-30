---
name: EN 50129 Signalling Safety
description: EN 50129:2018 Railway applications - Safety related electronic systems for signalling - THR to SIL mapping (Table A.1), fail-safety management of faults (Annex B formulas), SDT rules, component failure modes (Annex C), technique tables HR/R/-/NR per SIL (Annex E), UPICs for programmable logic (Annex F), QMR/SMR/TSR safety case, GPSC/GASC/SASC. Use for signalling system safety evidence, SIL derivation, fail-safety design or questions about EN 50129.
---

## When to use

Use for safety-related electronic systems (systems/subsystems/equipment) for railway signalling under EN 50129:2018: deriving SILs from THRs, fail-safety/fault management design rules, technique/measure selection per SIL, hardware random-failure and programmable-logic (UPIC) requirements, safety case structure and acceptance. Supersedes EN 50129:2003 and withdraws CLC/TR 50451:2007, 50506-1:2007, 50506-2:2009.

## Core knowledge

Read `reference/en-50129.md` for the complete structured reference (exact tables, formulas B.1–B.9, Annex E and F details) before making design or evidence decisions.

## Position in the framework

- Lives under **EN 50126-1/-2** life cycle (focus on phases 5–10); software safety integrity delegated to **EN 50128** (SIL inherited from 50126-2 derivation; SIL 0 = Basic Integrity).
- Safety-case categories: **GPSC** (generic product) → **GASC** (generic application) → **SASC** (specific application), SRACs carried forward.
- Safety case = 6-part structure with three mandatory reports: **QMR** (quality management), **SMR** (safety management), **TSR** (technical safety).

## THR → TFFR → SIL (Table A.1, exact)

All quantitative integrity is **random-failure (per-hour) integrity**; systematic failures are covered by the qualitative measures — both must be satisfied. Demand-mode systems are modelled as continuous rate models. There is **no Safe Failure Fraction column** (unlike IEC 61508).

| TFFR (h⁻¹) | SIL |
|---|---|
| 10⁻⁹ ≤ TFFR < 10⁻⁸ | SIL 4 |
| 10⁻⁸ ≤ TFFR < 10⁻⁷ | SIL 3 |
| 10⁻⁷ ≤ TFFR < 10⁻⁶ | SIL 2 |
| 10⁻⁶ ≤ TFFR < 10⁻⁵ | SIL 1 |
| TFFR > 10⁻⁵ | Basic Integrity |
| TFFR < 10⁻⁹ | split functions or SIL-4 measures + additional technical/operational measures |

## Annex B — fail-safety & fault management (normative formulas)

- **Double-fault FFR**: Eq B.1/B.2 — FFR = 2·FR²·SDT (two collaborating residual/dormant faults, detection-safe-down time SDT between them).
- **SDT bound**: Eq B.3 — SDT ≤ TFFR / (2·FR_A·FR_B) with per-item failure rates FR_A, FR_B.
- **Mü8004 rule** (Eq B.5/B.6): SDT ≤ k / (1000·(FR_A+FR_B)); k = 1 for 2oo2 (dual), k = 0.5 for 2oo3 (triple with 2 used).
- **Triple-fault condition**: Eq B.8 — SDT ≤ 2 / (FR_A+FR_B+FR_C); **Eq B.9** — measures against triple faults are NOT required if each item's FR ≤ 2·10⁻⁶/h.
- SDT rules include power-off/off-line credit (SDT/400-type factors, Table B.1) — read exact conditions in the reference before crediting.
- Single-fault condition must be handled by inherent fail-safety, composite fail-safety (redundancy with diverse channels → FTA/FMEA demonstration) or reactive fail-safety (detection + safe reaction within allowed time).

## Technique tables (Annex E, normative; HR/R/–/NR per SIL)

- Your SIL dictates which analyses/design/coding/testing measures are **HR** (highly recommended; deviation needs detailed rationale), R (recommended), – (neutral), NR (not recommended).
- Tables E.1–E.9 cover system behaviour, man-machine interface, hardware and software (the software rows delegate depth to EN 50128), plus approved combinations and proven-in-use criteria (≈10⁶ operating hours) — check the exact row set for your SIL in the reference before freezing the safety plan's technique list.

## Hardware & programmable logic

- **Annex C**: component failure-mode catalogues (C.1–C.15) for establishing inherent fail-safety at component level.
- **Annex F — UPICs** (tables F.2–F.8): unified programming implementation conditions for programmable logic (HDL, formal equivalence checking, static timing analysis, coding guidelines) when COTS/programmable devices enter safety functions.
- Hardware random integrity: allocate the TFFR over channels/equipment, verify via FTA against the apportioned targets (apportionment worked example in Annex D).

## Relation to other skills

- Process/programme: **`en-50126-1`**; THR/SIL derivation machinery and role independence: **`en-50126-2`**.
- Quantitative fault-tree verification of safety targets: **`iec-61025`**; FMECA for fail-safety demonstration: **`iec-60812`** / **`mil-std-1629a`**; random-failure rate math: **`iec-61703`**; failure-rate estimation from life data: **`iec-61649`**.
