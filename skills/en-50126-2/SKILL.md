---
name: EN 50126-2 Systems Approach to Safety
description: Apply EN 50126-2:2017 railway systems approach to safety - Hourglass model, risk assessment and hazard control split, risk acceptance principles (CoP/reference system/ERE), TFFR to SIL mapping (Table 2), THR apportionment formulas, role independence rules, ALARP/GAME/MEM acceptance criteria, safety case categories GPSC/GASC/SASC. Use for railway safety requirements specification, SIL/TFFR derivation or questions about EN 50126-2.
---

## When to use

Use for safety derivation and demonstration under EN 50126-2:2017: Hourglass model, RAP/RAC, THR→TFFR→SIL, apportionment formulas, independence, safety-case categories, risk matrix calibration references. (Process itself = `en-50126-1`; signalling equipment evidence = `en-50129`.)

## Core knowledge

Read `reference/en-50126-2.md` for the full structured summary including exact tables and formulas.

## Hard rules (per this part)

1. **Hourglass model (5.1)** separates: top (railway-system black box): System Definition → Risk Analysis → Risk Evaluation → **System Requirement Specification** at the waist → supplier side (system under consideration) hazard control: refined hazard identification + **causal analysis** + **Common Cause Analysis**. Human operators are NOT part of the technical system; their conditions are **application conditions**.
2. **Three RAPs** (8.3, gapless): Code of Practice (risks then acceptable; register requirements in hazard record) / Reference System (proven in use; must match functions, interfaces, operating and environmental conditions) / Explicit Risk Estimation (define RAC; methods ALARP, GAME, MEM are in Annex A — the standard itself doesn't set the criteria values).
3. **Acceptance-criteria methods (Annex A)**: **ALARP** (RSSB-style decision); **GAME** (French/STRMTG: modified system globally as safe as reference); **MEM** (Kuhlmann): natural death rate 2×10⁻⁴/yr; ≤5% per system across ≤20 systems ⇒ **10⁻⁵ fatality/(person·year)**; **DRA** curve extends tolerability for many-fatality accidents (down toward 10⁻⁹–10⁻¹⁰ at ~100–200 fatalities). Equivalent weighting **1 fatality ≈ 10 major ≈ 100 minor** injuries.
4. **SIL = for electronic functions only.** Never allocate SIL to mechanical/pneumatic/hydraulic (treat as not-applicable — use CoPs and technology standards instead; 10.2.1/10.3). SILs aren't attributes of a system (never "SIL 4 computer"; correct: "computer capable of the specified SIL 4 functions provided associated SRACs are applied").
5. **TFFR ↔ SIL (Table 2, exact)**: 10⁻⁹ ≤ TFFR < 10⁻⁸/h → **SIL 4**; 10⁻⁸ ≤ TFFR < 10⁻⁷ → **SIL 3**; 10⁻⁷ ≤ TFFR < 10⁻⁶ → **SIL 2**; 10⁻⁶ ≤ TFFR < 10⁻⁵ → **SIL 1**; > 10⁻⁵ → Basic Integrity; < 10⁻⁹ → split functions OR implement SI.4 measures + other technical/operational measures. Table's quantitative attribution is **random-failure integrity only**; systematic failures are covered by SIL qualitative measures (not quantifiable) — both must be satisfied.
6. **Apportionment to the "last independent functions"** (10.2.2): functions Independently able to counteract the hazard, and no common-cause failure (random or systematic) can jeopardise. If only random CCF excluded → apportion random integrity but **SIL unchanged**; if both excluded from top level → SIL may be allocated at the lowest level. For multiple hazards per function use the **strictest** TFFR/SIL.
7. **THR/TFFR quantification links (Annex D.3)**: THR_A ≈ THR_X·THR_Y·(µX+µY)/(µX·µY) (OR-of-independent repairing functions); AND-gate product valid only for probabilities with λ·SDT ≪ 1: P_B·P_C = (1−e^(−λB·SDT_B))(1−e^(−λC·SDT_C)). Worked: THR_A = 10⁻⁹/h ⇒ THR_B ≈ 10⁻⁷/h with SDT_B = 15 years, THR_C ≈ 10⁻⁷/h with SDT_C = 12 h.
8. **Role independence (Clause 7)**: verifier/validation by entity not involved in producing the work; Validator independent from Project Manager; **SIL 3/4 → Validator shall not report to PM**; **ISA** (if required) independent from PM and all other project role entities; reduced independence structure allowed only if no credible direct fatality potential or **SIL ≤ 2**. Competence per Annex G role specs.
9. **Safety case categories (Clause 6)**: **GPSC** (generic product) → **GASC** (generic application) → **SASC** (specific application; may split into application design + physical implementation); SRACs carried forward; SASC accepted by RU/IM becomes part of their safety management system. Generic-product validation occurs at end of Phase 6 (first item) as well as Phase 9.
10. **Variability handling (8.4.2)**: worst possible scenario / reasonable estimates (recommended) / reasonable worst case.
11. **Technique table (Annex F.2)** per Basic Integrity and SIL: PHA HR everywhere; **FTA / Markov / FMECA / CCF analysis / cause-consequence diagrams / interface hazard analysis: HR at SIL 3/4, R at SIL 1/2**; HAZOP HR at 3/4; FTA and Markov mutually exclusive; R/event-tree/zonal/historical-event analysis R.
12. **Basic Integrity (10.2.11)**: lightest regime — ISO 9001 + operator training + maintenance manuals; no SIL qualitative measures; no safety case required; self-assessment acceptable; no ISA beyond the initial allocation check; non-intrusiveness of BI functions on SIL functions must be shown.
