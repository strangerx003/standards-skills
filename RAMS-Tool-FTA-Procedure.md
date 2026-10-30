# RAMS Tool — FTA Generation Procedure (IEC 61025:2006 compliant)

**Document purpose:** Functional procedure specification for a RAMS tool that generates and quantifies fault trees using the methodology of IEC 61025:2006 (2nd edition). Written so that developers can implement it directly and RAMS engineers can validate it step by step.

**Standard basis:** IEC 61025:2006, all formula references in this document are to clause numbers of that standard. Prior knowledge assumed: completed Hazard Analysis and FMECA for the system under analysis.

**Status:** Working procedure. Each clause reference below allows verification against the standard.

---

## 1. Tool overview

The tool produces, for one analysis project:

1. A defined **scope and top event** (one tree = one top event),
2. A constructed **fault tree** (symbols per IEC 61025 Clause 4 / Annex A),
3. A **minimal cut set** list (qualitative evaluation — Clause 7.5.4.2),
4. A **quantified top-event probability** with importance ranking (7.5.4.3),
5. An **FTA report** (Clause 9 minimum content),
6. A **traceability register** tying every element back to design data, FMECA, hazard analysis and data sources (Clauses 6.2 + 8).

Tool roles: FTA analyst (system knowledge + FTA training), independent reviewer (design engineer, per clause 6.1), data owner (reliability data).

---

## 2. Project data model (what the tool stores)

| Object | Fields (mandatory) | Basis |
|---|---|---|
| Analyses project | name, system ID, standard version, analyst, reviewer, status | 6.1 |
| Analysis (one tree) | top event, scope, boundaries, resolution level, assumptions list, mission profile, status | 6.1, 7.5.3 |
| Event | type (basic / undeveloped / conditional / dormant / house / intermediate / zero), identifier, description (what + when), parent gate, probability, probability type (p / λ / λ+T / λT/2+λT_R / distribution), data source ref, FMECA ref, hazard ref | 3, 4, 8 |
| Gate | type (OR, AND, VOTE m-of-n, XOR, NOT, NOR, NAND, INHIBIT, PAND, SEQ, SPARE), inputs (events/gates), output event | 4, Annex A |
| Data record | event ID, value, unit (per-hour or per-demand), source, applicability statement, review status | 7.6, №9 report content |
| Label register | event ID ↔ design doc reference ↔ FMECA line ↔ hazard ID | Clause 8 |
| Result | cut sets, Q_S, importance ranking, sensitivity results, approximation validity check | 7.5.5 |
| CCF record | common-cause group member IDs, CCF factor used, justification | 8, 5.2 |

**Naming rules (Clause 8):** event ID = hierarchical code + component + failure mode, e.g. `PM1_CONTACTS_CLOSED_T>60S`; repeated/common events share identical identifiers (tool blocks duplicates); different failure modes of one item remain distinguishable (`Short_C132` vs `Open_C132`).

---

## 3. Procedure (tool workflow, step by step)

### Phase I — Frame

**Step 1 — Create analysis record**
Input fields: scope, objective, boundaries (what is in / out), system description, failure definition, operational modes, operational profile (trains/day, demand rates, mission time), maintenance regime (test interval T, repair time T_R), environment conditions, human factors model.
*Validation: tool shall not proceed to tree editing before all Clause 6.2 inputs have an entry (may be "explicitly not applicable" with justification).*

**Step 2 — Define the top event**
Free text + structured record. Template guidance depending on the analysis goal:
- Safety analysis → dangerous condition, precisely worded ("Signal … shows PROCEED while route locked as conflicting…", "…section reported CLEAR while occupied…"),
- Reliability/availability analysis → inability to deliver the defined function in the operational mode.
Exactly **one** top event per tree (tool constraint).

**Step 3 — Set resolution level**
Choose: component-level / assembly-level / sub-system-level. Tool stores this; later checks flag every basic event whose granularity disagrees with the recorded resolution.

**Step 4 — Set the review checkpoint**
Tool marks analysis as "constructed pending review" — clause 6.1 requires design-team review of the finished tree before quantification is issued.

### Phase II — Construct the tree

**Step 5 — Build top-down, immediate-cause discipline**
Tool workflow for every event box:

1. Display the event description.
2. Prompt the analyst: *"Can this fault consist of a component failure?"*
   - **Yes** → insert OR gate → the tool generates automatically the three standard child inputs: **primary fault** (failure in design envelope) / **secondary fault** (unqualified environment) / **command fault** (proper functioning, wrong time). Analyst completes or removes unused branches with justification.
   - **No** → free construction: analyst adds the minimum immediate, necessary and sufficient causes through the relevant gate(s).
3. Repeat per input, one level at a time (complete each gate before developing its children).
4. Terminate a branch when: basic event reached (data available) / undeveloped event justified / transfer to another page (same label).

**Step 6 — Gate selection rules the tool enforces**

| Situation | Gate | IEC basis |
|---|---|---|
| Multiple independent causes, each sufficient | OR | Annex A.3 |
| Redundant elements, failure needs all | AND | Annex A.3 |
| Voting / k-of-n architecture (e.g. 2oo3 safety computer) | VOTE (m = n−k+1) | Annex A.3 |
| Occurrence conditional on a circumstance | INHIBIT (condition on ellipse) | Annex A.3 |
| Order of occurrence matters | PAND / SEQ | Annex A.4 |
| Standby redundancy | SPARE | Annex A.4 |
| Exact-one-of-two | XOR | Annex A.3 (use restricted per standard) |
| Complement logic | NOT / NOR / NAND | restricted to experienced analysts — tool requests qualification flag |
| Load sharing / common environment | dynamic gate or CCF handling — tool blocks naive AND | 7.5.2.4 |

**Step 7 — Event↔state consistency check (6.1.2)**
Tool validation plug-in at save time:
- outcome is an *event* ⇒ all AND-gate inputs must be events;
- outcome is a *state* ⇒ all AND-gate inputs must be states;
- an OR-gate input may be either, but the tool flags mixed OR-fan with events/list-state mixed items for manual confirmation.

**Step 8 — Labelling & cross-reference**
Every new event writes one line into the Label Register (event ID ↔ document reference ↔ FMECA line ↔ hazard ID). Repeated event insertion is always performed by **reference to the existing ID**, never by copying text.

### Phase III — Qualitative evaluation

**Step 9 — Structural checks (tool automatic)**
- No gate-to-gate connection without an intermediate event box (7.5.3; violation = data model inconsistency).
- Every gate has ≥ 2 meaningful inputs (except null gate, allowed, stored as 1-input OR).
- No isolated events.
- Repeated events: identical label only; tool computes the replication list.

**Step 10 — Boolean reduction → minimal cut sets (7.5.4.2)**
Tool algorithm (successive substitution, equivalent to MOCUS referenced by IEC through its bibliography):

1. Write one Boolean equation per gate (OR = `+`, AND = `·`).
2. Substitute top-down; expand by distributive law.
3. Prune: idempotence (`XX→X`) and absorption (`A+AB→A`) after every expansion.
4. Result: `T = M1 + M2 + … ` in minimal product terms.
5. Output: cut-set list sorted by order; order-1 cut sets auto-flagged as **single point failures** (the tool asks the analyst for design justification or marks them for FMEA cross-check).

**Step 11 — Common-cause / common-event screen**
Tool scans cut sets (order ≥ 2) for repeated identifiers and for same-component/same-environment attributes (same type, same location, same test interval, same maintainer, same power source). Founds a **CCF group**; adds a CCF basic event per group with a beta-factor split per the data owner's instruction; justifies each group in the CCF record.

**Step 12 — FMEA cross-check (5.4.1)**
Import the FMECA; the tool compares:
- each FMECA single failure that reaches the top event ↔ must appear as an order-1 cut set;
- each order-1 cut set ↔ must exist in the FMECA.
Deviations are listed as open findings (one of the two analyses missed an event).

### Phase IV — Quantitative evaluation

**Step 13 — Data attachment (7.6)**
Per basic/undeveloped event: probability or rate, type, source, applicability justification. Where the source provides rates and the tree is mixed, the tool converts **all rates to probabilities first** (IEC's recommended path for mixed trees):

| Component situation | q formula |
|---|---|
| Continuous operation, exponential | q = 1 − e^(−λt) ≈ λt for λt ≤ 0.1 |
| Repairable, monitored | q = λT_R/(1+λT_R) ≈ λT_R |
| Periodically tested (interval T, repair T_R) | q ≈ λT/2 + λT_R |
| Per-demand, n demands | q = 1−(1−p)^n ≈ np for np ≤ 0.1 |

Tool state requirement: every basic event carries q with source before quantification allows running.

**Step 14 — Cut-set quantification**
For each minimal cut set: `Qi = ∏ q_k` (independence verified per CCF screen; else the CCF branch already restructured the tree in Step 11).

**Step 15 — Top-event combination. Tool computes all three and reports an approximation validity statement:**

| Method | Formula | When valid / purpose |
|---|---|---|
| **Rare event** | Q_S ≈ Σ Q_i | all Q_i ≤ 0.1 and Σ ≤ ~0.1; error < ~10%, **conservative** (default) |
| **Esary–Proschan** | Q_EP = 1 − ∏ (1−Q_i) | upper bound when overlap is material |
| **Exact (disjointing / BDD)** | expand by relative complements to make all terms disjoint, then add; or build BDD of the tree | needed whenever rare-event sum > 1 or events are not "small"; validated on the standard's own bridge network example to reproduce the RBD value |

**Step 16 — Dynamic gates (PAND / SEQ / SPARE)**
Tool routes these to an internal Markov solver (IEC 61165 basis) or simulator; the resulting probability is inserted back as **one basic event** with its Markov-model reference recorded (Clause 5.4.3 pattern). Cut-set enumeration excludes dynamic branches unless the analyst explicitly accepts an order-ignoring approximation with justification.

**Step 17 — Importance ranking (5.2, 5.4.4)**
- Cut set importance: `Fi = Qi / Q_S` — ranked table (this is the reported Pareto).
- Basic event importance: `ek = (Σ over cut sets containing k of Qi) / Q_S` — identifies the components to attack first.
- Exact figures via BDD where the tool supports it.

**Step 18 — Sensitivity (5.2)**
One-click variations: each q {×2, ×0.5, ×10}; plus "what if order-1 cut set removed" design case. Output: tornado chart + the design questions answered ("does duplicating component X remove the dominant cut set?").

### Phase V — Report (Clause 9)

**Step 19 — Generate report**, minimum content per the standard:
1. Objective and scope (incl. what was excluded)
2. System description with boundaries
3. Assumptions (design / operation & maintenance / reliability model) — including the approximation-validity statement from Step 15
4. Analyst/team, expertise; **top event definition and criteria**
5. Data references for **every** basic and undeveloped event, with applicability justification
6. Analysis description: data, symbols used, common-cause treatment, **minimal cut sets**
7. Results: Q_S (and method used), importance ranking, sensitivity conclusions
8. Conclusions and recommendations (design actions per dominant cut sets)
9. Optional annexes: diagrams, R&M data summary, FMECA cross-reference table

**Step 20 — Review loop**
Tool routes analysis to the design-team reviewer (6.1). Status transitions: Draft → Constructed → Reviewed → Quantified → Issued. Agreed corrective actions are recorded and tracked to closure within the tool.

---

## 4. Built-in validation checklist (tool-internal gate; each analysis must pass before "Issued")

| # | Check | Ref |
|---|---|---|
| V1 | Exactly one top event; no ambiguous wording | 3, 7 |
| V2 | All clause 6.2 inputs recorded (or justified N/A) | 6.2 |
| V3 | All events labelled; repeated events share IDs; no duplicate labels; IDs traceable to design docs | 8 |
| V4 | Event/state consistency in AND gates | 6.1.2 |
| V5 | No gate-to-gate; each gate fully defined before development | 7.5.3 |
| V6 | Cut sets generated and pruned to minimal | 7.5.4.2 |
| V7 | Every basic event has q + source + applicability | 7.6, 9 |
| V8 | CCF groups identified; identical redundancies not naively multiplied | 8 |
| V9 | Approximation validity stated (rare-event conditions met, else EP/exact used) | 7.5.5 |
| V10 | Dynamic branches solved via Markov/sim, result reinserted | 5.4.3, A.4 |
| V11 | FMECA cross-check findings closed | 5.4.1 |
| V12 | Report contains all clause 9 minima | 9 |
| V13 | Reviewer sign-off recorded | 6.1 |

---

## 5. Reference case validation (the tool's own acceptance test)

The tool's quantification engine shall reproduce IEC 61025 Clause 7.5.5 bridge-circuit example exactly:

- Cut sets: ab, cd, aed, bec
- Rare event (deliberately invalid here): 1.002 (>1 — engine must **reject** and warn, not output)
- Esary–Proschan: 0.708 (conservative bound)
- Exact (disjointing per Annex B): **0.656**, equal to the RBD ground truth.
A tool that reproduces all four numbers is compliant for the static-gate domain; the dynamic gate engine is separately validated against its Markov model of the standard's PAND diode example (Annex A, Figure A.1).

---

## 6. Out-of-scope statements (per the standard)

- Selection of raw failure-rate data sources is outside IEC 61025 — the tool therefore treats data entry as an external input with **source + applicability** as mandatory provenance, never a generic library value without justification.
- Repairable-system dynamic availability (beyond the steady-state, independent-repair forms of 7.6) is handled by the tool's Markov module on the basis of IEC 61165, flagged as an IEC-61165 extension rather than an IEC-61025 claim.
- Software fault probabilities: not derivable; tool models software-derived failure as undeveloped events with qualitative arguments unless the project has a defensible quantification basis.
