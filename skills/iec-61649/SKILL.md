---
name: IEC 61649 Weibull Analysis
description: Weibull analysis per IEC 61649:2008 - life data analysis with 2- and 3-parameter Weibull, median rank regression plotting, Benard plotting positions, MLE parameter estimation, confidence intervals for beta/eta/B-lives, censored and suspended data handling, mixed populations, goodness-of-fit. Use for Weibull plotting, failure data analysis, B-life estimation or questions about IEC 61649.
---

## When to use

Use for analysing life-to-failure data (time, cycles, distance, stress applications) with the Weibull methods of IEC 61649:2008 (2nd ed.): probability plotting, median rank regression, MLE parameter estimation, confidence bounds, censored/suspended data, 3-parameter fits, mixed populations, and interpretation (infant mortality vs random vs wear-out).

## Core knowledge

Read `reference/iec61649.md` for the complete method set (exact equations, worked examples, MLE formulas, interval tables) before computing anything beyond the basics below.

## The distribution (exact forms)

- PDF/CDF: `F(t) = 1 − exp[−(t/η)^β]` (two-parameter; add location `t₀` for three-parameter).
- Hazard: `λ(t) = (β/η)(t/η)^(β−1)`.
- **β (shape)**: β=1 → exponential (constant rate); β>1 → wear-out; β<1 → infant mortality.
- **η (characteristic life)**: F(η) = 0.632 for every β.
- `B_p = η·[−ln(1−p)]^(1/β)`; MTTF = η·Γ(1+1/β).

## Method selection (Table 1 of the standard — respect it)

- **Graphical (MRR/median-rank)**: all data kinds incl. small samples (≤20), multiple censored, curved data.
- **MLE**: singly censored or complete data, large samples only; **not covered** for interval/multiple censored or small samples.
- **WeiBayes** (prior β): zero-failure data, small samples, interval censored.
- Estimation from as few as 2 failures is possible but uncertainty is excessive — always plot confidence limits.

## Plotting procedure (median rank regression)

1. Rank failure times; X = time, Y = median rank. Median ranks: `BETAINV(0.5, J, N−J+1)` or Benard's approximation `F_i = (i−0.3)/(N+0.4)`.
2. **Suspended (censored) items**: use adjusted ranks (Leonard-type recursion with suspension adjustment — exact recursion in the reference); a suspension raises the ranks of subsequent failures only.
3. Linearize: `ln[−ln(1−F)] = β·ln(t) − β·ln(η)`; fit by regression (Y-on-X per the standard's guidance), β̂ = slope, η̂ = −intercept/slope-exp.
4. Curvature check: convex/concave curvature → consider 3-parameter Weibull (needs physical justification for t₀ + preferably ≥21 failures; only use with technical justification).

## Estimation & confidence

- MLE: solve the two-parameter likelihood (exact equations in the reference; Mann–Schafer–Singpurwalla) — biased at small n, use graphical check.
- Confidence intervals for β, η, and B-lives: analytical (χ², likelihood-ratio) or graphical (5%/95% rank bands via `BETAINV`).
- Goodness of fit: r² of the MRR line; treat low r² as evidence of a non-Weibull population.
- Worked validation (in the reference): dataset gave MLE β̂ = 2.0906, η̂ = 83.80, B10 = 28.56 vs published 2.091/84/28.63 — use to smoke-test your own MLE implementation.

## Interpretation doctrine

- A straight-ish line = single Weibull population. Broken/curved plot or two slopes = mixed populations (competing failure modes) — separate by failure mode and analyse each with its own suspensions-set, or identify the S-type distribution.
- Failures of other failure modes count as **suspensions** for the mode of interest.
- Never assume a failure-free period (t₀) without physical argument.
- Always state the data type (operating time vs calendar time vs cycles) — renewal ("bad-as-old") assumptions for repairable systems change the interpretation.

## Relation to other skills

- Convert fitted (β, η) into R(t)/A(t)/MTBF math via **`iec-61703`**.
- Life-test planning and statistical test principles: IEC 60300-3-5 (referenced by this standard).
- Reliability apportionment/programme context: **`en-50126-1`**; hazard-rate feeds into THR/TFFR arguments via **`en-50126-2`** and FTA quantification in **`iec-61025`**.
