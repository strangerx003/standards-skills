---
name: MIL-STD-882E System Safety
description: Apply MIL-STD-882E Change 1 system safety practice - the 8-element process, 25 tasks (100/200/300/400-series), risk assessment (severity cats 1-4, probability A-F, RAC matrix), software safety (SCC/SwCI/LOR), hazard tracking system, risk acceptance. Use for DoD system safety work, hazard analyses, or questions about MIL-STD-882E.
---

## When to use

Use for system safety engineering per MIL-STD-882E (Change 1, 27 Sep 2023): program planning, hazard analysis tasks, risk assessment, software safety, hazard tracking, or reviewing compliance of a program against the standard.

## Core knowledge

Read `reference/mil-std-882e.md` for the full structured summary before answering. Content comes from the actual MIL-STD-882E Change 1 document.

## Key rules to always honour

1. **Mandatory content = Sections 3 & 4 only.** Tasks (Section 5, 25 total: 101–108, 201–210, 301–304, 401–403) apply only when cited in the contract. Never claim task applicability without contract citation.
2. **Severity categories** (Table I): 1 Catastrophic (death/permanent total disability/irreversible significant environmental/≥$10M loss), 2 Critical (permanent partial disability/≥3 hospitalized/reversible significant/≥$1M–$10M), 3 Marginal (lost work days/reversible moderate/≥$100K–$1M), 4 Negligible (no lost days/minimal/<$100K).
3. **Probability levels** (Table II): A Frequent → E Improbable (<10⁻⁶) → F Eliminated. Procedures, training, warnings, PPE **cannot** achieve F.
4. **RAC matrix** (Table III) gives High / Serious / Medium / Low. Tables I–III mandatory unless tailored alternatives are formally approved per DoD Component policy and derived from these tables.
5. **Design order of precedence** (4.3.4): eliminate → design alteration → engineered devices → warning devices → procedures/training/PPE last. Never use procedures/PPE as sole mitigation for Catastrophic/Critical severity.
6. **Software**: risk is assessed as severity × degree of software control (SCC 1–5 → SwCI 1–5 → LOR tasks; Tables IV–VI). Unmet LOR tasks force a documented risk level to PM accept-or-fund. SwCI 1 is *most* critical.
7. **Risk acceptance**: authorities defined in DoDI 5000 series; user representative formal concurrence required for all **Serious and High**. Acceptance must precede exposure; post-fielding new risks re-accepted. Use "initial", "target", and "event" risk vocabulary.
8. **Hazard Tracking System (HTS)**: closed-loop, with the minimum data elements in `reference/mil-std-882e.md` (causal factor, initial/target/event RAC, mitigations, V&V, acceptance record with authority + user concurrence, audit trail). Government gets government-purpose rights to HTS data.
