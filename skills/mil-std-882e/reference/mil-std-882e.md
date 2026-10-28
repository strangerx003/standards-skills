# MIL-STD-882E (Change 1, 27 Sep 2023) — System Safety Standard Practice — Full Reference

## 1. Scope & intent
- DoD **Systems Engineering approach** to eliminating hazards and minimizing risks where elimination isn't possible; applies to systems/products/equipment/workspace (hardware and software) across the whole life-cycle (design, test, production, use, disposal).
- Aligned with DoDI 5000 series, which defines **risk acceptance authorities** (the standard itself does not name who accepts risk).
- **Mandatory parts: Sections 3 (definitions) and 4 (general requirements) only.** Tasks (Section 5) are optional — each must be cited in the contract to apply; no task imposes requirements for other tasks.
- Integrates across SE disciplines (fire protection, occupational health, environmental, CHMR, etc.). System safety personnel aren't responsible for other disciplines' hazard management (4.2.2), but disciplines using this methodology must comply with §4.3/4.4 (4.2.3.1) — one discipline's mitigation may create hazards in another.

## 2. Eight-element system safety process (§4.3)
1. Document the system safety approach (incl. technical requirement flow-down and closed-loop HTS).
2. Identify and document hazards (full life-cycle, HW/SW/interfaces/human/environment) in the HTS.
3. Assess and document risk (severity + probability → RAC via Tables I–III; document numerical probability definitions).
4. Identify and document mitigation measures (design order of precedence; estimate risk reduction).
5. Reduce risk (implement via SE/IPT; present at technical reviews).
6. Verify, validate and document risk reduction (analysis/test/demo/inspection).
7. Accept risk and document (per DoDI 5000 authorities; user rep formal concurrence for Serious & High).
8. Manage life-cycle risk (HTS retained post-fielding; support Class A/B mishap investigations per DoDI 6055.07).

## 3. Risk assessment

### Severity (Table I)
| Cat | Name | Criteria (any one) |
|---|---|---|
| 1 | Catastrophic | Death; permanent total disability; irreversible significant environmental damage; loss ≥ $10M |
| 2 | Critical | Permanent partial disability; injuries/illness hospitalizing ≥3 personnel; reversible significant environmental; loss ≥$1M<$10M |
| 3 | Marginal | Lost work days; reversible moderate environmental; loss ≥$100K<$1M |
| 4 | Negligible | No lost work days; minimal environmental; loss <$100K |

### Probability (Table II)
| Level | Name | Individual item | Fleet/inventory |
|---|---|---|---|
| A | Frequent | Often in item's life | Continuously experienced |
| B | Probable | Several times | Frequently |
| C | Occasional | Sometime | Several times |
| D | Remote | Unlikely but possible | Unlikely but reasonably expected |
| E | Improbable | May not occur (<10⁻⁶) | Unlikely but possible |
| F | Eliminated | Incapable of occurrence | Incapable |

Doctrine, training, warnings, cautions, PPE **cannot** move a hazard to F. Appendix A example numeric bands: A ≥10⁻¹, B 10⁻¹–10⁻², C 10⁻²–10⁻³, D 10⁻³–10⁻⁶, E <10⁻⁶.

### Risk Assessment Matrix (Table III) — RAC = severity + probability
| Prob\Sev | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| A | High | High | Serious | Medium |
| B | High | High | Serious | Medium |
| C | High | Serious | Medium | Low |
| D | Serious | Medium | Medium | Low |
| E | Medium | Medium | Medium | Low |
| F | Eliminated | | | |

Risk levels: **High, Serious, Medium, Low**. Tables I–III mandatory unless tailored alternatives are formally approved per DoD Component policy and derived from these tables. Probability assessed per-hazard across all system modes; **event risk** assessed separately for events (DT/OT, demos, fielding).

### Design order of precedence (4.3.4)
a. Eliminate hazard through design selection → b. Reduce risk via design alteration → c. Engineered features/devices → d. Warning devices → e. Signage, procedures, training, PPE (avoid as sole mitigation for Catastrophic/Critical severity).

## 4. Software contribution to risk (§4.4)
Risk assessed as **severity × degree of software control** (no reliable software failure-rate data).

### Software control categories (Table IV) → SCC1 most critical
1. **Autonomous (AT):** autonomous control, no safe detection/intervention possible.
2. **Semi-Autonomous (SAT):** time for independent safety mechanisms to intervene; or displays safety-critical info needing immediate operator action.
3. **Redundant Fault Tolerant (RFT):** software issues commands that another entity completes; redundant independent fault-tolerant mechanisms.
4. **Influential:** generates safety-related info for operator decisions, no action required.
5. **No Safety Impact (NSI).**

### Software criticality (Table V) → SwCI → LOR
Rows SCC1–5 × severity 1–4:
- SCC1 → SwCI1, SwCI1, SwCI3, SwCI4
- SCC2 → SwCI1, SwCI2, SwCI3, SwCI4
- SCC3 → SwCI2, SwCI3, SwCI4, SwCI4
- SCC4 → SwCI3, SwCI4, SwCI4, SwCI4
- SCC5 → SwCI5 (all)

**LOR by SwCI:** 1 = requirements+architecture+design+code analysis + in-depth safety-specific testing; 2 = req/architecture/design + testing; 3 = req/architecture + testing; 4 = safety-specific testing only; 5 = none.

**Table VI:** if a SwCI's LOR tasks are unspecified/incomplete, document software contribution as High (SwCI1) / Serious (SwCI2) / Medium (SwCI3) / Low (SwCI4) and route to PM to fund LOR or formally accept risk. All software contributions in HTS. Criticality ≠ risk (Appendix B). FHA (Task 208) → SCC → SwCI → LOR chain embedded in SDP/STP. Appendix B also gives candidate causal-factor risk criteria (no interlock remaining = High; interlock boundary counts escalate) and suggested design requirements (fault tolerance/detection/isolation/annunciation/recovery, N-version, partitioning).

## 5. The 25 tasks (Section 5)

### 100-series — Management (101–108)
- **101 Hazard Identification & Mitigation Effort:** integrate into SE; resources/roles/flow-down to subs/vendors; report at SRR/PDR/CDR/TRR/PRR; closed-loop HTS incl. subcontractor data; IMS progress.
- **102 System Safety Program Plan (SSPP):** scope/objectives, interfaces, organization, milestones, safety requirements/criteria, hazard analysis process, HTS, analyses/techniques, SoS integration, HAZMAT, software approach, supporting data, V&V, audits, training, incident reporting.
- **103 Hazard Management Plan (HMP):** same content, discipline-neutral (Change 1 addition).
- **104 Government Reviews/Audits Support:** support safety boards and mishap investigations.
- **105 IPT/WG Support:** membership, hazard status, mitigation effectiveness consensus.
- **106 Hazard Tracking System:** establishes the HTS (tasks 108/204/205/206/207/210 add data elements).
- **107 Hazard Management Progress Report:** periodic status vs. milestones.
- **108 Hazardous Materials Management Plan (HMMP):** HAZMAT categorized prohibited (Gov approval required) / restricted (target elimination) / tracked; tracked data: name, category, SMCC (DoD 4100.39-M Vol 10), location, quantity with design traceability, application, life-cycle quantities, controls/training/PPE/MSDS.

### 200-series — Analysis (201–210)
- **201 Preliminary Hazard List (PHL):** concept-phase list from legacy mishap data, lessons learned, test docs, NEPA/EO 12114, disposal plans.
- **202 Preliminary Hazard Analysis (PHA):** initial risk assessment; ~20 consideration areas incl. components, energy sources, ordnance, HAZMAT, interfaces/controls, SoS interfaces, material compatibility, inadvertent activation, COTS/GOTS/NDI/GFE, software (software safety design criteria: inadvertent command, failure to command, untimely command, wrong magnitude), environment, procedures, modes, health, environmental impacts, human factors, life support/egress, event-unique hazards, infrastructure, SoS malfunctions. Per-hazard initial RAC + candidate mitigations per precedence.
- **203 System Requirements Hazard Analysis (SRHA):** derive/flow design requirements into specs & test plans; assess compliance at PDR/CDR; define V&V per requirement.
- **204 Subsystem Hazard Analysis (SSHA):** equipment level; requirement compliance & flow-down; failure modes, single point/common mode failures, human error; COTS/GOTS/GFE/NDI/software; updated after changes.
- **205 System Hazard Analysis (SHA):** integrated system level; subsystem interrelationships, independent/dependent/simultaneous events, degradation, design-change effects, human error, software contributions; verify mitigations introduced no new hazards.
- **206 Operating & Support Hazard Analysis (O&SHA):** EMD onward; operational/support procedures, facilities, tools, environment; PPE, warnings/cautions, packaging/handling/storage/transport, training; feeds tech manuals & training.
- **207 Health Hazard Analysis (HHA):** chemical/physical (acoustic, vibration, acceleration, barostress, heat/cold, shrapnel)/biological/ergonomic; non-ionizing (RF/laser, hazard distances) and ionizing radiation; HAZMAT evaluation (CAS/NSN/MSDS, usage, disposition); ergonomics; noise/vibration vs MIL-STD-1474/1472, ISO 2631; mitigation + target RAC per hazard.
- **208 Functional Hazard Analysis (FHA):** classify functions and consequences of failure/degradation/out-of-sequence; RAC; identify SCFs/SCIs/SRFs/SRIs mapped to HW/SW/human architecture; assign SCC & SwCI; produce fault-tolerance/detection/isolation/annunciation/recovery requirements. Done early.
- **209 System-of-Systems Hazard Analysis (SoSHA):** unique SoS hazards only; traceability to architecture, interfaces, data, stakeholders.
- **210 Environmental Hazard Analysis (EHA):** life-cycle environmental hazards, HAZMAT, demil/disposal, public exposures, noise, emissions; supports NEPA/EO 12114.

### 300-series — Evaluation (301–304)
- **301 Safety Assessment Report (SAR):** comprehensive hazard/risk status before test/operation/next phase/contract end.
- **302 Hazard Management Assessment Report (HMAR):** discipline-neutral SAR; adds explosives classification/EOD discussion.
- **303 Test & Evaluation Participation:** TEMP inputs, test-unique mitigations, Safety Releases, post-test analysis.
- **304 Review of ECPs, Change Notices, Deficiency Reports, Mishaps, Deviation/Waiver Requests:** full process applied to each change/mishap.

### 400-series — Verification (401–403)
- **401 Safety Verification:** analysis, test, demo (incl. induced/simulated failures); substitutes (analogy, lab, mockup, simulation) when test infeasible.
- **402 Explosives Hazard Classification Data:** DAEHCP/TB 700-2 data.
- **403 EOD Data:** ordnance functioning/safety, render-safe/disposal data, training aids.

## 6. HTS minimum data elements
Hazard; system; subsystem; applicability (version-specific HW/SW); requirements references; system mode; causal factor (HW/SW/human/environment); effects; mishap; initial RAC; target RAC; event RAC(s); identified and selected mitigations (traceable to versions); hazard status; V&V method; action org/person; record of risk acceptance (authority + user concurrence title/org, date, document location); hazard management log (audit trail); HAZMAT elements. Closed-loop; contractor + Government access; government purpose rights to HTS data and supporting analyses.

## 7. Risk acceptance
- Authorities per DoDI 5000 series; supporting configuration documentation provided to Government for life-cycle retention.
- Acceptance before exposure to known hazards; tables define risk at the decision point unless tailored.
- User representative formal concurrence for all **Serious and High** acceptances.
- Event risks accepted at multiple life-cycle points; post-fielding new/revised risks re-accepted.

## 8. Tailoring
- Cite task numbers; use each task's "details to be specified" ((R) items required from Government). Contractors may propose task changes with rationale in proposals.
- Risk-matrix tailoring only with formal approval; derived from Tables I–III; same for software Tables IV–VI (SSCM tailoring must meet/exceed Table V LOR).
- Appendix A Table A-I: task applicability by phase (MSA/TD/EMD/P&D/O&S; G generally, S selectively, GC for design changes, N/A). Highlights: management tasks generally applicable all phases; SSHA/SHA/SoSHA not applicable in MSA, general in EMD/P&D; PHA mostly MSA; O&SHA selective MSA, general through P&D; 303 general everywhere except selective O&S; verification N/A in MSA, general in P&D.
- Prioritise tasks vs budget/schedule considering complexity, dollar value, expected risk.
