---
name: IEC 60300-3-3 LCC
description: Apply IEC 60300-3-3:2017 dependability management life cycle costing - LCC process, cost breakdown structure, discounting/NPV/IRR formulas, NRC/RC categories, uncertainty and sensitivity, dependability-to-LCC trade-offs. Use for LCC analysis, program economics, life cycle costs and questions about IEC 60300-3-3.
---

## When to use

Use for performing or reviewing Life Cycle Costing per IEC 60300-3-3:2017 (Ed 3.0): LCC of systems with dependability-driven costs, LCC comparisons of alternatives, cost breakdown structures, discounting/inflation treatment, or questions about the standard.

## Core knowledge

Read `reference/iec60300-3-3.md` for the complete structured summary before analysis.

## Key doctrine

1. **LCC = total cost incurred during the life cycle** (acquisition + ownership + disposal); covers only expense elements (tangible + intangible, incl. **allowance for residual risk**), not revenue (financial trade-offs follow after).
2. **Six life-cycle stages** (A.1): concept → development → realization → utilization → enhancement → retirement; first three = **acquisition costs**, last three = **ownership costs** (typically exceed acquisition and are largely *committed early* — ~35/75/95/99/100% committed by end of each acquisition/realization/utilization/enhancement stage).
3. **Main purpose = comparing alternatives** where future ownership cost is significant: reliability ↑ raises acquisition but lowers O&S; **an optimum reliability at minimum LCC exists**; availability optimization is critical because unavailability drives consequential costs (lost revenue, alternative service, warranty, liability). **LORA** (level-of-repair analysis) is the canonical acquisition ↔ utilization trade-off.
4. **Process (Clause 5)**: establish context → plan the analysis (scope/objectives; criteria NPV/payback/IRR) → define approach (**CBS = 3-D matrix: work breakdown structure × life-cycle stages × cost categories** [labour, materials, fuel/energy, overheads, transport]) → perform (estimate — parametric/analogous/engineering methods; collect/validate; aggregate = simple sum; sensitivity; independent review) → finalize (follow-up actions with named owners; documentation: traceability, validation).
5. **Discounting** via DCF/NPV (C.2) and IRR (C.3); the discount rate **contains an inflation component**; designate the **base date** first; deduct indirect VAT-type taxes from market prices; depreciations are usually **excluded** for LCC; GAAP usual or IFRS alternative; include early-dependability-investment opportunity costs.
6. Estimating methods (5.5.1): parametric, analogous, engineering builds — with worked standard examples; all alternatives must be run through the **same model** (5.4.2); exclude costs common to all options.
7. **Uncertainty & sensitivity (5.4.4/5.5.4)**: two uncertainty elements (model assumptions; data accuracy) with four inaccuracy sources — stochastic reliability data (MTBF-type), planned O&M balance, indeterminate future recovery costs, and **untreated unrealized risk cost**; use ranges or PDFs; Monte Carlo permitted.
8. Modelling caution: LCC models compare scenarios; do not compare structurally different models across alternatives.
