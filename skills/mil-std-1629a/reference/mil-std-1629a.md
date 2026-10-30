# MIL-STD-1629A — FMECA — Full Reference

MIL-STD-1629A, 24 Nov 1980 (supersedes MIL-STD-1629(SHIPS) 1974, MIL-STD-2070(AS) 1977). Approved for all DoD departments/agencies; Navy custodian (Naval Air Engineering Center, Lakehurst); Army/Air Force review. OCR of the scanned PDF — worksheet figures (Figs 101.1–104.1) are garbled as images but every column is spelled out in task text.

## 1. Scope & applicability
- Purpose: systematically evaluate and document, by item failure-mode analysis, the potential impact of each functional or hardware failure on **mission success, personnel/system safety, system performance, maintainability, and maintenance requirements**; each potential failure ranked by severity of effect.
- Applies to acquisition of all designated DoD systems/equipment, primarily during **demonstration & validation and full-scale engineering development**; also production/deployment. **Does NOT apply to software.**
- **Iterative, early, updated**: started as soon as preliminary design information is available at higher system levels, extended downward as data becomes available; major consideration at every design review; recommended actions formally dispositioned or rationale documented.
- Coincident use planned (§4.3.6) with MIL-STD-785 (reliability), 470 (maintainability), 882 (safety), 2072 (survivability), 1388 (LSA), 2080 (MPA), 1591 (fault diagnosis) — identify responsible organizations, preclude duplicated analyses.
- Tasks numbered from 101; referenced as standard number + task number(s); revisions lettered (e.g., 101A).

## 2. The tasks
| Task | Title | Dependency |
|---|---|---|
| 101 | FMEA | baseline |
| 102 | CA | supplements 101; not imposed without 101 |
| 103 | FMECA-Maintainability Information | requires 101 |
| 104 | DMEA (damage modes, hostile threat) | requires 101 |
| 105 | FMECA Plan | required if 101 required; may merge into MIL-STD-785 plan |

**FMEA approaches (101 §3)**: hardware (from drawings, normally bottom-up), functional (functions analyzed, normally top-down), or combination. Can start at any indenture level, proceed up or down.

## 3. Planning & contributing data
- **Planning (§4.3)**: worksheet formats (minimum info of Figs 101.3, 102.1, 103.1, 104.1); initial indenture level on each sheet header; ground rules & assumptions (approach, lowest indenture level, performance criteria defining failure, added assumptions documented separately); coding system based on hardware breakdown/MIL-STD-780 work unit codes, traceable to block diagrams; failure definitions.
- **Indenture-level selection (§4.3.3)**: lowest level in the LSA candidate list; lowest level at which items will get Category I/II; the specified maintenance/repair level for Cat III/IV items.
- **Contributing info (§4.4.1)**: specs & development plans (block diagrams, mission/environmental profiles, time-stress relations); trade-off reports; design data/drawings; reliability data — same equipment test data preferred, else **MIL-HDBK-217** or similar-item field experience.
- **FMEA process (§4.4.2)**: define system → block diagrams → identify all failure modes & effects → evaluate worst consequence → severity class → detection methods & compensating provisions → corrective actions → effects of actions → document.

## 4. Single-item rules (Task 101 §4)
Analyze each failure as the only failure; if non-detectable, extend to a second failure combined with it that produces Cat I/II; passive and multiple failure combinations leading to Cat I/II identified; assumptions broadened for safety/redundancy items; all single failure points flagged; module performing a block-diagram function gets its own FMEA "viewed as a system."

## 5. Criticality Analysis (Task 102)
Rank each failure mode by combined severity classification and probability of occurrence. Two approaches:

### Qualitative — failure probability levels
A Frequent >0.20; B Reasonably probable >0.10<0.20; C Occasional >0.01<0.10; D Remote >0.001<0.01; E Extremely unlikely <0.001. (With these levels, remaining CA columns not required; go to the criticality matrix.)

### Quantitative
- λp source = the reliability prediction's source; **MIL-HDBK-217 default** (λb + all adjustment factors πA, πE, πQ...).
- **Severity (§4.4.3):** I Catastrophic (death or weapon system loss); II Critical (severe injury, major property/system damage, **mission loss**); III Marginal (minor injury/damage, delay/availability loss/mission degradation); IV Minor (unscheduled maintenance or repair).
- **β:** Actual = 1.00; Probable = 0.10≤β<1.00; Possible = 0<β≤0.10; No effect = 0.
- **α:** Σα = 1 per item; from failure-rate/test data or judgment.
- **t:** per-mission-phase operating hours/cycles from the system definition.
- **Cm = β·α·λp·t**; **Cr = Σ Cm** over all modes of the item in one severity class; ratio pro item may include ×10⁶ scale adjustment (Appendix A 50.6).
- **Criticality matrix** (severity × probability level or Cr): IDs plotted; **farther up the diagonal = more critical**. Completed matrix in the FMECA report. Criticality numbers are relative ranking indicators only.
- **Worked example (A.6 §50.6):** λb=0.10×10⁻⁶/h; factors 1.5, 40, 1.2 × ... → λp = 7.2×10⁻⁶/h; Cat II modes α₁=0.3, α₂=0.2; β=0.5; t=1h → Cm₁ = 1.08, Cm₂ = 0.72, **Cr = 1.80**.

## 6. Worksheet columns

### FMEA (Fig 101.3, Task 101 §5)
1 Identification number (block-diagram-traceable) · 2 Item/functional identification · 3 Function · 4 Failure modes and causes (all predictable modes, each with all probable independent **causes**, within adjacent indenture levels; check against the six generic modes) · 5 Mission phase/operational mode · 6 **Failure effects**: local / next higher / end (end may arise from **double failure** — flag) · 7 **Failure detection method** (visual/audible, automatic sensing, instrumentation, Normal/Abnormal/Incorrect "other indication"; isolation procedure; ambiguity vs same symptoms) · 8 **Compensating provisions**: design items (redundancy, safety/relief monitoring/alarm devices, standby/alternative modes) and operator actions (with consequences of probable incorrect operator actions) · 9 Severity classification (I–IV) · 10 Remarks (design-improvement recommendations, effects of redundant item failures, unusual conditions, criticality design features). Acceptance rationale for surviving Cat I/II: design tolerance/derating, test, inspection, history.

### CA (Fig 102.1)
Columns 1–6 same as FMEA + 7 failure probability/failure rate data source · 8 β · 9 α · 10 λp · 11 t · 12 Cm · 13 Cr (**severity-class-ordered**). Filed after FMEA at same indenture level.

### FMECA maintainability (Fig 103.1, Task 103)
+ failure predictability (incipient indicators, data to collect, tests/inspections), failure detection means (organizational technician level, indenture localization, ambiguity resolution, monitoring/warning, BIT capability, ancillary test equipment), basic maintenance actions (corrective actions, modular replacement, follow-on adjustment/calibration), remarks.

### DMEA (Fig 104.1, Task 104)
+ damage modes (threat mechanisms: penetration, severed, shattered/cracked, jammed, deformed, burned out — electrical overload, burn-through; conditional dependency; cascading) and damage effects + remarks (redundancy, separation, fire-path elimination, integral armor; test; history).

## 7. Block diagrams
**Functional block diagram** (Fig 101.1): operations & interrelationships, functional flow per system and per indenture; MIL-M-24100 guidance. **Reliability block diagram** (Fig 101.2): series dependence of all functions per life-cycle event; MIL-STD-756. All I/O shown/labeled, each block with consistent item number per functional breakdown order for traceability through indenture levels.

## 8. Key definitions (§3)
Failure mode; failure cause; failure effect (local/next higher/end); **single failure point** (uncompensated by redundancy or alternative procedures); **undetectable failure** (no detection means making the operator aware); detection mechanism; compensating provision; corrective action; interface (external power/cooling/heating/signal suppliers); severity (worst potential consequence); criticality = relative measure of consequence × frequency of occurrence; Cm; Cr; damage mode; primary/secondary damage effects; threat mechanism. Base vocabulary from MIL-STD-280, 470, 721, 780, 785, 882, 1388.

## 9. FMECA report (§4.5)
Level of analysis; results summary; data sources/techniques; system definition; worksheets grouped highest level first; ground rules & assumptions diagrams. Interim reports at each design review highlight Cat I/II modes, single failure points, proposed corrections. **Final report reflects final hardware** and lists Cat I/II modes and single failure points not eliminated. Contents: summary (conclusions/recommendations/omitted-item rationale) + **reliability critical item lists** — (a) Cat I & II failure-mode list, (b) single failure points list with criticality class; each list entry: item ID+cross-ref; design features minimizing failure; verification/detection tests; planned inspections; design history; operator detection method/detectability of redundant-mode failure.

## 10. Appendix A — Application & tailoring
Ordering data (task numbers, indenture, report level, DID DI-R-7085/7086); tailoring by deletion/addition; application criteria: lower indenture = more detail; **"a timely low-detail FMECA beats a late detailed one"**; timing tied to decision points; CA most valuable for maintenance/logistics prioritization; criticality numbers only relative. Ordering per task: also the DIDs. Forms: DD 1426 improvement proposal.
