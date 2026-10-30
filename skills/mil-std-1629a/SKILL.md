---
name: MIL-STD-1629A FMECA
description: Perform FMEA and Criticality Analysis per MIL-STD-1629A - FMA/FEA/CA/DMEA tasks, severity categories I-IV, failure probability levels A-E, criticality numbers Cm/Cr formulas, worksheet formats, criticality matrix. Use for FMECA work per the military standard, or questions about MIL-STD-1629A.
---

## When to use

Use this skill for performing, reviewing, or interpreting FMEA/FMECA under MIL-STD-1629A (24 Nov 1980): the 5 tasks, worksheet columns, criticality analysis math (Cm/Cr), severity classifications, and criticality matrix. (Note: for railway/automotive FMEA under IEC 60812, use the `iec-60812` skill — different RPN conventions.)

## Core knowledge

Read `reference/mil-std-1629a.md` for the full structured summary (all task procedures, worksheet columns, worked example numbers) before analysis.

## The 5 tasks

- **101 FMEA** — baseline: hardware, functional, or combined approach; failure modes/causes, local→next-higher→end effects, detection, compensating provisions, severity class.
- **102 CA** — Criticality Analysis; **shall not be imposed without Task 101**. Qualitative (probability levels A–E) or quantitative (Cm/Cr).
- **103 FMECA-Maintainability Information** — maintenance-oriented extension (failure predictability, detection means, basic maintenance actions).
- **104 DMEA** — Damage Mode and Effects Analysis for hostile-threat (combat) conditions.
- **105 FMECA Plan** — contractor's implementation plan (often folded into the reliability program plan).

## Hard rules to always honour

1. **Iterative and early**: FMECA starts as soon as preliminary design info exists at higher levels and extends downward; untimeliness is the standard's stated chief cause of ineffective FMECA. Update after each design change; presented at every design review.
2. **Severity categories** (I–IV, deliberately matching MIL-STD-882): **I Catastrophic** (death/weapon-system loss), **II Critical** (severe injury/major damage/mission loss), **III Marginal** (minor injury/damage, mission delay/degradation), **IV Minor** (unscheduled maintenance only).
3. **Single-failure discipline**: each failure analysed as the *only* failure in the system; if a single failure is **non-detectable**, the analysis extends to a **second failure** that with it could produce a catastrophic/critical condition. All single failure points uniquely flagged.
4. **Failure modes considered** (checklist of six generic modes): premature operation; failure to operate at prescribed time; intermittent operation; failure to cease operation at prescribed time; loss of output/failure during operation; degraded output; other unique conditions.
5. **Corrective-action priority**: elimination of Category I & II modes first; if not eliminated, alternatives go to the procuring activity with documented rationale (design factors/derating, test, inspection, history).

## The criticality math (quantitative CA)

Data source: same as the contract reliability prediction — default MIL-HDBK-217 rates (base λb with all π adjustment factors). Coefficients:

- **β** (failure effect probability): 1.00 actual loss; 0.10–<1.00 probable loss; 0–≤0.10 possible loss; 0 no effect.
- **α** (failure mode ratio): fraction of λp attributable to the mode; **Σα = 1** over all modes of an item.
- **λp**: part failure rate from the prediction.
- **t**: operating time/cycles in the mission phase.

$$C_m = \beta\cdot\alpha\cdot\lambda_p\cdot t \qquad C_r = \sum_{n=1}^{j}(C_m)_n \text{ (over modes of one severity class)}$$

Scale by 10⁶ for entry convenience (table entries like "1.08" = 1.08×10⁻⁶). **Criticality numbers are for relative ranking, not absolute probability.** Worked example (Appendix A 50.6): λp = 7.2×10⁻⁶/h, β=0.5, α₁=0.3, α₂=0.2, t=1 h → Cm₁ = 1.08, Cm₂ = 0.72, Cr = 1.80 (Category II).

**Qualitative alternative:** probability levels A Frequent (>0.20), B Reasonably probable (0.10–0.20), C Occasional (0.01–0.10), D Remote (0.001–0.01), E Extremely unlikely (<0.001).

**Criticality matrix:** severity (horizontal) vs probability level or Cr (vertical); the farther along the diagonal from origin, the greater criticality and urgency. Completed matrix goes in the report.

## RPN does not exist in this standard

No S×O×D concept. Ranking = severity classes × probability levels (qualitative) or Cm/Cr (quantitative) with the diagonal criticality matrix. Software is explicitly out of scope.

## Report/lists (§4.5)

FMECA report includes summary with conclusions/recommendations, list of omitted items with rationale, and **reliability critical item lists**: (a) Category I & II failure modes list; (b) separate **single failure points** list with criticality classification; each critical item entry covers design features minimizing failure, verification/detection tests, planned inspections, design history, operator detection method.
