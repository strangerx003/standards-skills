# Standards Skills

Skills that make any AI agent an **instant expert on a published engineering standard**. Each skill encodes the complete content of one standard — its procedures, symbols, formulas, tables, worked examples and mandatory rules — not just pointers to it. Installing a skill means the agent can *perform* the standard exactly as prescribed, not merely cite it.

Each standard is a **separate, standalone skill**. Mix and match: install one, several, or all.

## The skills

| Skill ID | Standard encoded | Domain | Expertise installed |
|---|---|---|---|
| [`iec-61025`](skills/iec-61025/SKILL.md) | IEC 61025:2006 (2nd ed.) | Fault Tree Analysis | Both FTA methods, all event/gate symbols with exact formulas, immediate-cause construction, Boolean reduction, minimal cut sets, Annex B disjointing, labelling rules, report requirements |
| [`mil-std-882e`](skills/mil-std-882e/SKILL.md) | MIL-STD-882E (with Change 1) | System Safety | 8-element process, all 25 tasks, severity/probability/RAC matrices, design order of precedence, software safety (SCC→SwCI→LOR), HTS data elements, risk acceptance, tailoring |
| [`nureg-0492`](skills/nureg-0492/SKILL.md) | Fault Tree Handbook (US NRC) | Fault Tree Analysis (in-depth) | Five ground rules, fault taxonomy, Boolean/probability foundations, cut-set quantification equations (Tables XI-2/XI-3), importances, common cause, pressure-tank and three-motor examples, failure-rate data |
| [`mil-std-1629a`](skills/mil-std-1629a/SKILL.md) | MIL-STD-1629A (1980) | FMECA | Tasks 101–105, all worksheet columns, severity categories I–IV, probability levels A–E, Cm/Cr criticality math (β·α·λp·t), criticality matrix, single-failure-point discipline, report/critical-item lists |
| [`iec-60812`](skills/iec-60812/SKILL.md) | IEC 60812:2006 (2nd ed.) | FMEA/FMECA | Design & process FMEA procedure, worksheet design, RPN scales and the standard's own RPN cautions, criticality matrix and number, CCF/human/software factors, FMEA↔FTA selection |
| [`iec-60300-3-3`](skills/iec-60300-3-3/SKILL.md) | IEC 60300-3-3:2017 (Ed 3.0) | Life Cycle Costing | LCC process, 3-D cost breakdown structure, NRC/RC categories, discounting/NPV/IRR, estimate methods, uncertainty & sensitivity, dependability↔LCC trade-offs incl. worked examples |
| [`iec-61703`](skills/iec-61703/SKILL.md) | IEC 61703:2016 (Ed 2.0) | RAM Math | Full equation set: R(t)/A(t), MTTF/MTBF/MTTR/MDT distinctions, renewal & alternating-renewal processes, Markov systems, exponential closed forms, production availability, maintenance-support decompositions |
| [`iec-61649`](skills/iec-61649/SKILL.md) | IEC 61649:2008 (2nd ed.) | Weibull Analysis | 2-/3-parameter Weibull, median rank regression & Benard positions, adjusted ranks with suspensions, MLE with validated worked numbers, confidence limits, WeiBayes/table-1 method selection, mixed populations |
| [`en-50126-1`](skills/en-50126-1/SKILL.md) | EN 50126-1:2017 | Railway RAMS (process) | 12 life-cycle phases with activities/deliverables, RAM & Safety plans, Hazard Log, risk acceptance principles (CoP/reference/ERE), S1–S5 severity, THR, safety case 6-part structure, FRACAS |
| [`en-50126-2`](skills/en-50126-2/SKILL.md) | EN 50126-2:2017 | Railway RAMS (safety methods) | Hourglass model, TFFR↔SIL Table 2, THR/TFFR apportionment formulas (Annex D), ALARP/GAME/MEM criteria, role independence & ISA rules, GPSC/GASC/SASC, Annex F technique tables |
| [`en-50126-3`](skills/en-50126-3/SKILL.md) | CLC/TR 50126-3:2006 | Rolling Stock RAM | FailI/FailS/FailM failure categories, FR/MTBF/MTTF/MDBF target tables, maintainability & availability target templates, LRU breakdown structure, RAM programme, demonstration/burn-in/warranty rules |
| [`en-50129`](skills/en-50129/SKILL.md) | EN 50129:2018 | Signalling Safety Systems | TFFR↔SIL Table A.1, fail-safety/fault-management formulas (Annex B, B.1–B.9), component failure modes (Annex C), HR/R/–/NR technique tables (Annex E), UPICs for programmable logic (Annex F), QMR/SMR/TSR safety case |

Each skill is a self-contained folder:

```
skills/<skill-id>/
├── SKILL.md          ← when to use + the standard's hard rules + workflow
└── reference/*.md    ← the complete internalised content of the standard
```

## Compatibility

Skills are ordinary Markdown files with frontmatter — no agent-specific dependencies. Any AI that can read files can use them:

- Agents with a skills system that auto-discovers `SKILL.md` directories: copy a skill folder into that system's skills location and it is advertised and loadable by ID.
- Agents without a skills system: direct the agent once — *"Load `skills/<id>/SKILL.md`, then read `reference/*.md` fully before answering anything about this standard."* From then on it treats the standard as its own knowledge.

## Install

**Shared host (one user, applies to every project):** copy the folders you want from `skills/` into the host's global skills directory.

**Per project/repo:** copy into the project's skills directory (e.g. `skills/`, `.opencode/skills/`, `.claude/skills/`, `.agents/skills/` — whatever your host uses, the folder containing `SKILL.md` is the skill).

**Direct from this repo (no clone needed):** your skills catalog can load straight from this URL, which serves the catalog `index.json`:

```
https://raw.githubusercontent.com/strangerx003/standards-skills/master/skills/
```

For example, in a configuration supporting URL catalogs:

```jsonc
{ "skills": ["https://raw.githubusercontent.com/strangerx003/standards-skills/master/skills/"] }
```

## Verify the install

Ask the agent a check question; an expert must answer:

| Ask | Expert answer must contain |
|---|---|
| "Series system → which IEC 61025 gate and formula?" | OR gate, F_S = 1 − ∏(1−Fᵢ) |
| "Can PPE alone close out a Catastrophic MIL-STD-882E hazard?" | No — severity 1 requires design-level mitigation; PPE is last in precedence, cannot reach probability level F |
| "Give me the NUREG-0492 ground rules." | All five: fault written with what/when, component-vs-system rule, no miracles, complete-the-gate, no gate-to-gate |
| "TFFR of 5×10⁻⁸/h → which SIL?" | SIL 3 — 10⁻⁸ ≤ TFFR < 10⁻⁷ (EN 50126-2 Table 2 / EN 50129 Table A.1) |
| "Two dormant faults with failure rates FR·FR and detection-safe-down time SDT — the FFR?" | FFR = 2·FR²·SDT, with the SDT bound from Annex B of EN 50129 |
| "50126-3's three failure categories?" | FailI (Significant/Immobilising), FailS (Major/Service), FailM (Minor) — with the customer-specified delay/cost thresholds |
| "Median rank of the 2nd failure out of 8?" | 0.2024 — Benard's (2−0.3)/(8+0.4) per IEC 61649 |
| "MIL-STD-1629A: is RPN used for ranking?" | No — severity I–IV × probability A–E or Cm/Cr criticality numbers on the criticality matrix; no S×O×D in this standard |

## Adding a new standard

1. Drop the source document (PDF) in the repo root — it stays as ground truth.
2. Extract its full text (embedded text via `pypdf`, or OCR via `pypdfium2` + `tesseract` for scans).
3. Read the full document, then write `skills/<id>/SKILL.md` (when-to-use, hard rules, workflow) and `skills/<id>/reference/<id>.md` (complete structured summary: equations, tables, examples).
4. Add the entry to `skills/index.json` (bump `version`) and to the table above.
