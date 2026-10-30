---
name: EN 50126-3 Rolling Stock RAM
description: Apply CLC/TR 50126-3:2006 - rolling stock RAM guide to EN 50126-1 - customer/supplier RAM specification, FailI/FailS/FailM failure categories, FR/MTBF/MTTF/MDBF reliability targets, maintainability and availability target tables, RAM programme, demonstration/burn-in/warranty, vehicle breakdown structure via LRUs. Use for rolling stock RAM requirements, demonstrations or questions about 50126-3.
---

## When to use

Use for specifying or demonstrating **rolling stock RAM** under CLC/TR 50126-3:2006 (informative guide to EN 50126-1, invoked on the 1998 edition's 14 phases — reminder: that edition has 14 phases, not the 12 of EN 50126-1:2017): RAM requirements specification, failure categories, reliability/maintainability/availability targets, RAM programme and in-service demonstration, tender evaluation.

## Core knowledge

Read `reference/en-50126-3.md` for the complete tables (Tables 4–19) and templates before writing requirements or a demonstration plan.

## Scope guardrails (the TR is explicit)

- **Covers RAM only** — Safety is limited to a rolling-stock hazard reference list (its Clause 7); LCC limited to RAM parameters. Use `en-50126-1`/`en-50126-2` for the safety process and `en-50129` for signalling equipment evidence. It contains **no MTBSAF/MTBUR/availability-UR-IR/TFFR/SIL machinery** — don't credit it with those.
- **No numeric RAM target values** — it's a guideline *process* for choosing values (from similar-stock past performance + realistic improvement), with example templates only.
- Lives from invitation to tender through demonstration in operation; applicable to new as well as modified/refurbished stock; "system" = whole rolling stock down to component.

## Failure categories (Table 4 — the backbone of all targets)

- **FailI Significant/Immobilising**: delay > specified time and/or cost > specified level; rolling-stock-specific triggers: train stopped on track, not allowed into service, withdrawn from service.
- **FailS Major/Service**: must be rectified to achieve specified performance, but does NOT breach the Significant thresholds; e.g. failure of listed functions (door system per side, coach lighting, air-conditioning, toilet count).
- **FailM Minor**: neither significant nor major; leads to a maintenance task even with no service impact.
- Customer must state: delay minutes per category, cost thresholds, **delay-counting method**, and specific conditions deemed train-stop/withdrawal. Failures counted per category against targets plus chargeable/non-chargeable rules.

## Reliability targets (Table 8)

- Per rolling stock + per subsystem, per category (subscripts I/S/M): **max accepted FR** (per million km or hours) and **min accepted MTBF** (repairable) / **MTTF** (non-repairable) / **MDBF** in km. MTBF ↔ MDBF conversion needs a predefined average speed from the Mission Profile.

## Maintainability / availability targets

- Maintainability (Tables 9–12): qualitative essay requirements (accessibility, dismounting, modularity → two-level maintenance: swap LRU on train, repair off train; handling — no item > one-person weight unless two-person; testability...), quantitative preventive/corrective (MinInt, MaxST, MaxMMH, MaxAT, FC, MTTR, MTTM, MTBM), logistic support (MaxAT reach/plan, SOR spares-on-stock probability, TAT, lead time), maintenance cost (T/SP/PM/CM; per-vehicle/per-seat bases).
- Availability (Table 13, EN 50126-1 Annexes A/C based): use the standard's definitions with the guide's symbols/formulas — exact set in the reference.

## RAM programme & demonstration

- RAM Programme owned by **both** customer and main supplier; main supplier owns content/plan; configuration management by main supplier (customer's own CMS from Phase 10 into service).
- Breakdown structure: functional (criticality analyses) vs physical/logistic (maintainability; last level = **LRU**); 3–4 levels recommended; Annex A worked examples.
- Demonstration (6.1.3): chargeable vs non-chargeable failure rules, burn-in credit, **≥2-year steady-state** field data, warranty terms, RAM Demonstration Plan. Apportionment not prescribed — supported by RBD, FTA, functional FMECA and LRU rate aggregation (sum of LRU rates × quantities).

## Relation to other skills

- Generic process and 2017 vocabulary/calibration: **`en-50126-1`**; safety derivation: **`en-50126-2`**; signalling equipment: **`en-50129`**.
- Reliability math and availability formulas: **`iec-61703`**; life-data fitting for MTBF/MDBF estimation in service: **`iec-61649`**; LCC model construction: **`iec-60300-3-3`**.
