---
name: IEC 61703 RAM Math
description: Reliable mathematical expressions for reliability, availability, maintainability and maintenance support terms (IEC 61703:2016). Use for availability/reliability math of repairable and non-repairable items, MTBF/MTTF/MTTR/MDT formulas, Markov models, renewal processes, exponential closed forms, production availability, or questions about IEC 61703.
---

## When to use

Use this skill for the *mathematics* of dependability: computing R(t), A(t), availability, MTTF/MTBF/MTTR/MDT, failure intensity, renewal processes, repairable-system Markov results, production availability, maintenance-support time decompositions — per IEC 61703:2016 (2nd edition). This is the standard's own formula engine; the full reference contains all equations.

## Core knowledge

Read `reference/iec61703.md` for the complete equation set (distribution tables, exponential closed forms, Volterra/recursion machinery, all worked examples) before using any formula outside the common ones below.

## The standard's structure (decide your case first)

- **Systems** (several individual items) → state-transition and Markov models (§6.1 of the standard).
- **Individual items**: (1) non-repairable — one random variable, time to failure; (2) repairable with negligible restoration time → renewal process; (3) repairable with non-zero restoration time → alternating renewal process.

## Key identity terms (use exactly as the standard defines)

- **MTTR = MFDT + MAD + MLD + MACMT** (fault detection time + administration + logistic delay + corrective maintenance time). Availability always ."
- **MUT + MDT = MTBF**; METBF = MUT+MDT = MTTF+MTTR (asymptotic case).
- **Asymptotic availability A = MUT / (MUT + MDT)**.
- **Production availability K(t)** — up-state fraction over production demand window; use instead of unavailability when the system has production modes.
- Vesely rate **λ_V = z / A**; failure intensity z(t) = A(t)·λ_V(t).
- The three canonical item classes each have closed forms under exponential λ and µ — tables in the reference cover R(t), z(t), A(t), U(t), means and asymptotes for **non-repairable / zero-restoration / non-zero-restoration** items (Annex C of the standard).

## Common traps (standard explicitly defines these)

1. **λ vs z vs λ_V** — constant rate λ applies to non-repairable items only; repairable items use intensity z(t) which converges to λ asymptotically but is not constant in general.
2. **MTBF ≠ MTTF** — MTBF counts occurrence of failure in repairable item (and nominally excludes up time preceded by nothing); MTTF is for non-repairable "first failure expected time".
3. Degradations of availability: **inherent A (no delays)**, achieved (with maintenance association MTTM), **operational/achieved-operational (includes logistic/administrative delays)**.
4. **Normal distribution not covered** by the standard's distribution tables (only exponential, Weibull, Gamma, Erlang, Rayleigh, lognormal + repair-time variants).
5. Warranty/reliability bounds: series/parallel/k-of-n system expressions are NOT given in this standard (delegated via IEC 61078 / IEC 61165); apply this standard for the single-item/intensity math only, then combine per that standard.
6. Multiple aggregation events with h i.i.d. and independent items: apply renewal/recursion machinery rather than pretending it stays exponential.

## Relation to other skills

- The ** railway availability targets (MUT/MDT) in `en-50126-1`** matter here — this skill provides the math engine behind Annex B Fig B.1 of EN 50126-1.
- For weibull data analysis on lifetime samples, pair with **`iec-61649`**; use this standard to convert the Weibull parameters into unavailability/availability functions over the mission.
