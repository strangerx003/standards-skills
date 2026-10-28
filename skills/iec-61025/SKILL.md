---
name: IEC 61025 Fault Tree Analysis
description: Apply IEC 61025:2006 Fault Tree Analysis - qualitative/quantitative FTA, symbols and gates, minimal cut sets, Boolean evaluation, labelling, reporting. Use for FTA work, reliability modelling, hazard analysis with fault trees, or questions about IEC 61025.
---

## When to use

Use this skill for any task involving fault tree analysis (FTA) under IEC 61025: designing fault trees, evaluating cut sets, computing top-event probabilities, interpreting FTA symbols/gates, integrating FTA with FMEA/ETA/Markov/BDD/RBD, or reviewing an FTA report against the standard.

## Core knowledge

Read `reference/iec61025.md` for the full structured summary of the standard before producing analysis, tables, or tree structures. Content comes from the actual IEC 61025:2006 2nd edition document (bilingual EN/FR).

## Workflow

1. Clarify the **method**: A (qualitative — cut sets with descriptive likelihood) or B (quantitative — event probabilities known).
2. Define **scope, boundaries, resolution** and the single unambiguous **top event** before structuring anything.
3. Construct top-down using the **"immediate cause"** and **"basic unit"** concepts (clause 7.5.3). Use correct event symbols and static/dynamic gates (per `reference/iec61025.md` Tables A.1–A.4).
4. Label every event uniquely and consistently (clause 8) — repeated/common-cause events carry *identical* labels; different failure modes of the same item must be distinguishable.
5. Evaluate: Boolean reduction → **minimal cut sets** → top-event probability. For static gates with shared events, note that rare-event/Esary-Proschan approximations have error; use the disjointing procedure of Annex B (or BDD) for exact results. Dynamic gates (PAND/SEQ/SPARE) need Markov analysis (IEC 61165).
6. Report per clause 9: objective/scope, system description, assumptions, analysts, event-probability references, minimal cut sets, results and recommendations.
7. If unsure which gate formula applies (NOT/XOR/NAND/NOR/series/parallel/k-of-n), look it up in the reference file — do not improvise.
