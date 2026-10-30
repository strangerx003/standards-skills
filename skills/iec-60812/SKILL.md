---
name: IEC 60812 FMEA/FMECA
description: Apply IEC 60812:2006 (2nd ed) - FMEA and FMECA procedure - design and process FMEA, failure mode/cause/effect analysis, severity/occurrence/detection scales, RPN and criticality matrix, CCF and human/software factors, worksheet design, FMEA-FTA relationship. Use for FMEA work under IEC 60812, or questions about the standard.
---

## When to use

Use for performing, structuring, or auditing FMEA/FMECA under IEC 60812:2006: procedure stages, worksheets, risk assessment scales, relation to FTA/RBD, process FMEA (PFMEA), or the standard's treatment of RPN. (For the military criticality-number approach use `mil-std-1629a`.)

## Core knowledge

Read `reference/iec60812.md` for the complete structured summary (procedure stages, tables, annex examples, RPN critique) before conducting or reviewing an FMEA.

## Key positions of the standard (never contradict these)

1. **Bottom-up, inductive, iterative**: FMEA identifies failure modes of every item and their effects up the hierarchy; start early in design, update as design matures; reusing another design's FMEA is valid only for identical use/stresses.
2. **Independence assumption**: each failure mode treated as independent → FMEA is unsuited to dependent/sequential failures — use FTA (IEC 61025) or Markov (IEC 61165) for those. Flag any mode that raises the probability/severity of another.
3. **Effect chain**: local effect → next-higher-assembly effect → end effect; a part's failure-mode *effect* becomes the next level's failure *mode* and *cause* (hierarchical propagation).
4. **End effects may arise from multiple failures** (e.g. safety device fails AND main function exceeds limits) — flag these on the worksheet; FMEA alone can't model them → escalate with FTA.
5. **Detection methods** and **compensating provisions** are analytical outputs, and evidence for design FMEA is design deficiency identification (review/analysis/simulation/test), for process FMEA process-control catch probability.
6. **Risk treatment options** (5.3): RPN = S×O×D (severity × occurrence × detection; higher D = less detectable) or the **criticality matrix** (severity × frequency classes E→A). State the time period; rates must account for the operational profile.
7. **RPN cautions (5.3.6.4 — the standard's own critique)**: ~88% of the scale unused, duplicates, nonlinear scaling, ordinal distortion; **with equal RPN, treat the higher-severity mode first**; severity 9–10 gets priority regardless of RPN; never compare RPNs linearly; review S, O, D individually.
8. **Criticality number approach (5.3.4)**: λi = αi·λj·βi; **C ≈ λi·tj**; **Ci ≈ λi·tj** (probability P ≈ 1−e^−C ≈ C for small C); "criticality number" is a risk measure, not a probability; only meaningful for the same indenture level.
9. **FMECA ≠ PRA**: for high-risk/high-complexity systems FMECA must not be the sole basis for risk acceptability — use probabilistic risk analysis (exposure time, avoidance probability, latency, fault detection).
10. **CCF (6.1)**: sources in design/manufacture/environment/human error; FMEA alone can't fully handle CCF — combine with functional diversity, physical separation, testing; note mitigations in Remarks.
11. **Human (6.2) & software (6.3)**: hardware FMEA must record HW–SW interrelationship explicitly; software changes may invalidate the FMEA; postulating software error effects has limited reach; fallback provisions emerge from the analysis.
12. **Report (5.4)**: summary + detailed record + block diagrams + **list of drawings with issue status**; effects summary table (Table 7/8-style) with per-mode failure references and probabilities per end effect for the stated period, profile and stresses.

## Recommended worksheet (Annex A.2)

Columns: item ref & description-function · failure mode · **failure-mode code** (unique ID) · possible failure causes · local effect · (optional next-higher column) · final effect · detection method (BIT or diagnostics — identify it) · compensating provisions (incl. maintenance/operator actions) · severity class · frequency/probability (per million hours, per 1 000 km, etc., with the period stated in the header) · remarks (unusual conditions, redundant-element failure effects, critical design features, sequential analysis cross-refs, maintenance implications, decisions taken e.g. at design review).

## Automotive scales (5.3.6, from SAE J1739 / AIAG 3rd ed.)

- Severity 1–10 (10 = hazardous without prior warning — safe-vehicle or regulatory non-compliance; 9 = hazardous with warning; ≤8 functional degradation grades).
- Occurrence 1–10 over the designated lifetime basis — must state the basis (e.g., ≤0.010/1000 = 1, ≥100/1000 = 10). **The scale is neither linear nor logarithmic** → RPN nonlinearity is inherent.
- Detection 1 = almost certain detection by design control → 10 = absolutely uncertain/no control. Process FMEA: probability current controls catch defect before next process/customer.

## FMEA vs FTA (7.4 + 4.2) — when to use which

- FMEA: comprehensive failure knowledge of items; smaller systems/modules; innovation design (no service history); many-component series logic.
- FTA (IEC 61025): all multiple-failure-mode and dependent systems; redundancy; complex logic; the standard recommends complementing FTA with FMEA-mode/effect detail; a full complex-system dependability analysis uses both.
