---
name: NUREG-0492 Fault Tree Handbook
description: Apply the NRC Fault Tree Handbook (NUREG-0492, Vesely/Goldberg/Roberts) - fault tree construction rules and ground rules, symbols, Boolean algebra, minimal cut sets, probability quantification, importances, common cause, and the classic pressure tank / three motor examples. Use for fault tree construction, teaching FTA methodology, or NRC-style safety analysis.
---

## When to use

Use for fault tree analysis methodology per NUREG-0492: constructing fault trees correctly (ground rules, immediate-cause procedure), relating trees to Boolean algebra, determining minimal cut sets, quantifying unavailability/reliability, importance ranking, or explaining FTA concepts (it is the classic teaching text behind IEC-style FTA).

## Core knowledge

Read `reference/nureg-0492.md` for the full structured summary before deep work. Content comes from the actual handbook (OCR'd, 210 pages).

## The five ground rules (always enforce)

1. **Ground Rule I:** every event box is written as a *fault*, stating precisely **what** (failed state) and **when** (system state making it a fault). Enlarge the box rather than truncate the description.
2. **Ground Rule II:** if the fault can be a component failure → *state-of-component* fault → OR-gate seeking **primary / secondary / command** modes; otherwise *state-of-system* fault → find minimum immediate necessary and sufficient causes (AND, OR, INHIBIT or no gate).
3. **No Miracles:** assume normal functioning propagates faults (no fortuitous failures block a sequence); but if normal functioning blocks propagation, include the AND structure that defeats it.
4. **Complete-the-Gate:** define *all* inputs to a gate before developing any of them (develop level by level).
5. **No Gate-to-Gate:** gate inputs must be properly defined fault events; never connect gates directly to gates during construction.

**Immediate-cause ("think small") procedure:** descend one step at a time, each step giving the *immediate, necessary and sufficient* causes — never jump to ultimate/root causes. Jumping skips "input present but component fails anyway" (basic failure) cut sets — the classic student error in the pressure tank example (leaping from rupture to the pressure switch, missing single-cut-set K2).

## Fault taxonomy

- **Failure** = basic abnormal occurrence (component fails in proper environment). **Fault** = higher-order event incl. proper operation at the wrong time. All failures are faults; not all faults are failures.
- **Primary fault:** failure within design envelope. **Secondary:** unqualified environment. **Command:** component functions but at wrong time/place (erroneous upstream signal).
- **Passive** components (pipes, welds, bearings) vs **active** (pumps, relays, valves) — failure rates typically 2–3 orders apart.
- **Mechanism → mode → effect** chain; the same event plays different roles per viewpoint (system man / subsystems man / component designer).

## Symbols

Circle = basic event; Diamond = undeveloped; Ellipse = conditioning event (PRIORITY AND, INHIBIT); House = normally-expected (non-fault) event; Rectangle = intermediate fault event; Triangles = transfer IN/OUT. Gates: AND (·), OR (+), INHIBIT (hexagon, special AND with conditioning event), PRIORITY AND (ordered sequence), EXCLUSIVE OR. Causality never passes through an OR-gate — inputs are re-expressions, not causes (diagnostic for bad tree logic).

## Key quantification (from the handbook)

- Gate probabilities: OR P = P(A)+P(B)−P(A)P(B|A) (mutually exclusive → sum; independent → pA+pB−pApB; fully dependent → max; sum always conservative). AND P = P(A)P(B|A).
- **Rare event approximation:** P(∪) ≈ ΣP → accurate within ~10% and conservative when probabilities ≲ 0.1. System Qₛ ≈ ΣQᵢ; Wₛ = ΣWᵢ.
- λ-model: F(t)=1−e^(−λt) ≈ λt for λt ≤ 0.1. Monitored repairable: q ≈ λT_R. Periodically tested: q ≈ λT/2 + λT_R. p-model per demand: q ≈ np.
- Importances: cut set importance Fᵢ = Qᵢ/Qₛ; component importance eₖ = Σ_{i∋k}Qᵢ/Qₛ.
- **Esary-Proschan / exact bounds / "signematics" are NOT in this handbook** — for exact quantification with shared events use disjointing/BDD per IEC 61025 or the NASA aerospace handbook; NUREG-0492 uses the conservative sum of truncated cut sets.
- Ordering-by-cut-set-size heuristic: each larger cut set order is typically ~3 orders of magnitude less probable.
- Data: WASH-1400 component failure rates (Table XI-1 in the handbook; e.g., motor fail-to-start 1×10⁻³/demand; relay 3×10⁻⁶–1×10⁻⁵/hr); order-of-magnitude precision expected, not more.

## Signature examples

- **Pressure tank (Ch. VIII):** top "rupture of pressure tank after start of pumping" → 5 minimal cut sets: K2, T(tank), S·S1, S·K1, S·R with Table VIII-1 data (P(E₁) ≈ 3.4×10⁻⁵; K2 = 86% importance → duplicate the relay; deeper lesson: monitor the *pressure*, add relief valve, remove timer; put AND-gates high in the tree to eliminate single-event cut sets).
- **Three motor test (Ch. IX):** 29 relays/timers/wiring example; E₅ and E₆ differ only in *when*-condition (K5 vs K3 contacts closed) — never merge them.
- **Common cause:** identical timers can collapse a quadruple cut set to effectively a double — use WASH-1400-style common-cause categories (manufacturer, location, environment, test/maintenance degradation, operator).

## Design lessons

AND-gates as high in the tree as possible (eliminate single-event cut sets); failure-space analysis preferred over success space; boundary/resolution choices determine comprehensiveness — implausibly tiny computed probabilities (10⁻¹⁶) signal omitted boundary events; monthly-maintenance unavailability (≈λT/2) can dwarf component failure probability.
