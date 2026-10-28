# NUREG-0492 — Fault Tree Handbook — Full Reference

Source: NUREG-0492, US NRC, Jan 1981, Vesely/Goldberg/Roberts/Haasl. Born from the NRC short course "System Safety and Reliability Analysis"; written in response to the Risk Assessment Review Group (NUREG/CR-0400) recommendation. (Retained in `source_ocr_fulltext.txt` alongside this file is the full OCR text of all 210 pages for verbatim lookup — treat as OCR-noisy, especially equations.)

## 1. Chapter structure

| Ch | Title | Contents |
|---|---|---|
| I | Basic Concepts of System Analysis | Decisionmaking context; system analysis = "a directed process for the orderly and timely acquisition and investigation of specific system information pertinent to a given decision"; boundaries/limit of resolution; inductive vs deductive |
| II | Overview of Inductive Methods | "What happens if–?": Parts Count, FMEA, FMECA, PHA, FHA, Double Failure Matrix, success path models |
| III | Fault Tree Analysis – Basic Concepts | Failure vs success space; choosing the top event |
| IV | Basic Elements of a Fault Tree | Full symbology (events, gates, transfers) |
| V | Fault Tree Construction Fundamentals | Faults vs failures, primary/secondary/command, mechanism/mode/effect, immediate-cause procedure, ground rules |
| VI | Probability Theory | Relative frequency, addition/multiplication rules, combinatorics, set theory, Bayes' theorem |
| VII | Boolean Algebra & Application to FTA | Rules, tree↔Boolean equivalence, Shannon expansion, minimal cut/path sets, top-down/bottom-up substitution |
| VIII | The Pressure Tank Example | Ends-to-end worked example, qualitative + quantitative |
| IX | The Three Motor Example | Larger example (relays, timers, wiring) |
| X | Probabilistic and Statistical Analyses | Binomial/normal/Poisson/exponential, failure-rate function, bathtub, Weibull, estimation, CIs, Bayes |
| XI | Fault Tree Evaluation Techniques | MCS, importances, common cause, unavailability/occurrence-rate quantification, Monte Carlo |
| XII | Fault Tree Evaluation Computer Codes | PREP, ELRAFT, MOCUS, MICSUP, ALLCUTS, SETS, FTAP, KITT1/2, SAMPLE, MOCARS, FRANTIC, ARMM, SAFTE, GO, NOTED, PATREC, WAM-BAM, PL-MOD, COMCAN, BACKFIRE |

## 2. Faults, failures, top event, scope

- **Top event:** an undesired (usually catastrophic) system event; not too general (unmanageable) or too specific (narrow). Deductive "Sherlock Holmesian" process.
- **Failure space preferred** over success space: easy consensus, fewer discrete modes, binary events (Minuteman: only 3 trees).
- Fault tree = model of the *credible faults contributing to one top event*, NOT all system failures. Implausibly tiny computed probabilities (10⁻¹⁶) signal ignored boundary/resolution events.
- Construction treats all systems as nonrepairable (fault *occurrence*); repair/existence enters only quantification (Ch XI).

## 3. Symbols (Table IV-1)

Primary events: **circle** basic event; **diamond** undeveloped; **ellipse** conditioning event; **house** normally-expected non-fault event; **rectangle** intermediate fault event. Transfer triangles: apex line = IN, side = OUT.

Gates (special cases of AND/OR):
- **AND (·):** inputs are the *causes* of output; for dependent inputs write "B given A".
- **OR (+):** inputs are re-expressions (more specific causes), NOT causes; causality through OR = missing AND / bad logic.
- **INHIBIT (hexagon):** special AND with an enabling conditioning ellipse (catalyst present; frozen line if T < T_freeze). Alternative form: ellipse holds P(Q occurs | A) for necessary-but-not-sufficient causes (secondary failures).
- **PRIORITY AND:** ordered sequence (order in ellipse). **EXCLUSIVE OR:** exactly one (inclusive OR is always the conservative choice; difference negligible at low p).

## 4. Fault taxonomy & construction

- **Primary:** failure in qualified environment (defective weld). **Secondary:** unqualified environment (overpressure). **Command:** operates properly but wrong time/place (upstream signal error).
- Passive (pipes, welds, bearings) vs active (pumps, relays, switches, valves): active ≳1×10⁻⁴/demand or ≳3×10⁻⁷/hr; passive 2–3 orders lower (WASH-1400).
- **Mechanism → mode → effect**; role varies by viewpoint (doorbell/fuel-flow examples, Tables V-1/V-2).
- Immediate-cause procedure and the five ground rules are in `SKILL.md`.

## 5. Probability theory (Ch. VI)

- P(E) = lim N→∞ N_E/N; addition rule; inclusion–exclusion P(A∪B) = P(A)+P(B)−P(A∩B).
- **Rare event approx:** P(∪Eᵢ) ≈ ΣP(Eᵢ); accurate ≲10% error and conservative when all p ≲ 0.1.
- Independent complements: 1−Π(1−pᵢ); (1−p)ⁿ when equal.
- Combinatorics: permutations (n)ᵣ; C(n,r); m-out-of-n binomial Σ C(n,k)pᵏ(1−p)ⁿ⁻ᵏ.
- Bayes' theorem P(Aᵢ|B) = P(B|Aᵢ)P(Aᵢ)/ΣⱼP(B|Aⱼ)P(Aⱼ) — "importance" P(Sᵢ|S) = P(Sᵢ)/ΣP(Sⱼ) ranks most likely failure modes posterior to an observed failure.
- Probability as a set-function (measure on the Borel field/class of subsets), independent of frequency-limit issues.

## 6. Boolean algebra (Ch. VII)

- Engineering notation: ∪→+, ∩→·, complement ′. Rules: distributive both forms, X+YZ=(X+Y)(X+Z); idempotent XX=X; absorption X+XY=X; complementation (XX′=∅, X+X′=Ω); de Morgan (X·Y)′=X′+Y′; X+X′Y=X+Y. Example: (A+B)(A+C)(D+B)(D+C) = BC+AD.
- Tree ↔ Boolean one-to-one: OR = "+", AND = "·". OR-gate probability P(Q)=P(A)+P(B)−P(A)P(B|A); cases: mutually exclusive → sum; independent → pA+pB−pApB; dependent → up to max(P). Sum always conservative. AND: P(Q)=P(A)P(B|A), max = min(P(A),P(B)) if dependent.
- **Shannon expansion:** 2ⁿ disjoint minterms; disjointness → exact quantification; canonical form ⇒ equality test.
- Restructuring: D=A(B+C) ≡ AB+AC; one unique minimal cut set form regardless of tree shape.

## 7. Minimal cut sets / path sets

- **MCS** = smallest intersection causing the top; a *failure mode*; top form T = M₁+…+Mₚ.
- Top-down substitution (start at top, expand, prune with idempotent + absorption; this IS the MOCUS algorithm) or bottom-up (MICSUP-style; gives MCS for every gate).
- Example: E₁=B+C, E₂=C+E₄, E₄=A·B → T = C + A·B.
- **Dual tree / minimal path sets:** complement via de Morgan or AND↔OR swap; path sets = success modes; T = C+AB → T′ = C′A′+C′B′.
- Cut-set counts explode: a 299-basic-event tree yields >64 million cut sets. Truncation (singles/doubles, like WASH-1400) common. Pressure tank full tree: 5 singles + 24 doubles; with secondary branches dropped: 3 singles + 10 doubles.
- Common cause (Ch. XI): code components by categories (manufacturer, location, seismic, flood, temperature, humidity, radiation, wear-out, test/maintenance degradation, operator interaction); a cut set whose members share the same category element is CCF-susceptible; identical timers can collapse K₃·KT₁·KT₂·KT₃ into a "double". Codes: COMCAN, BACKFIRE, SETS.

## 8. Quantification (Ch. XI) — key formulas

- λ-model (constant per-hour rate): F(t)=1−e^(−λt) ≈ λt (λt≤0.1). Standby+operating combined ≈ Fₛ+Fₒ for small values.
- p-model (per demand/cycle): q=1−(1−p)ⁿ ≈ np (np≤0.1).
- Monitored repairable unavailability: q = λT_R/(1+λT_R) ≈ λT_R.
- Periodically tested (interval T): q ≈ λT/2 + λT_R ≈ λT/2.
- Occurrence rate w(t) ≈ λ asymptotically; Nᵢ(t₁,t₂) = ∫Wᵢdt ≈ WᵢΔt; **Nᵢ ≤ 0.1 ⇒ Nᵢ ≈ unreliability**.
- Cut set unavailability Qᵢ = q₁q₂···qₙᵢ; system Qₛ ≈ ΣQᵢ; Wₛ = ΣWᵢ.
- Cut set occurrence rate Wᵢ = Σₖ(∏q except k)·w_k.
- Importances: Fᵢ = Qᵢ/Qₛ; eₖ = Σ_{i∋k}Qᵢ/Qₛ. Ordering heuristic: each extra cut set order ≈ 3 orders of probability.
- Handbook does NOT contain Esary-Proschan bounds/exact union methods; quantification = conservative rare-event sum over order-truncated cut sets (Table XI-2 collects all component/cut-set/system equations; Table XI-3 importances).
- Uncertainty via Monte Carlo (SAMPLE/MOCARS/FRANTIC).

## 9. Statistics (Ch. X)

- Binomial b(x;n,p), assumptions, mean/variance; extensions multinomial, negative binomial, hypergeometric (binomial OK if N≥10n). Example: p=0.01, n=10 → P(exactly 1) = 0.0913.
- Normal via z; ±1σ=68%, ±2σ=95%. Example: slot μ=0.9000″, σ=0.0030″, ±0.0050″ limits → 9.5% reject; σ′=0.0015″ for 0.1%.
- Poisson p(x)=mˣe^(−m)/x!; binomial approx (n=10,p=0.1: 0.3874 vs 0.3679).
- Exponential from Poisson/Markov: R(t)=e^(−λt); failure rate λ(t)=f/(1−F); bathtub: burn-in / constant-λ / wear-out. Rayleigh λ=kt; **Weibull** λ=ktᵐ → R(t)=exp(−kt^(m+1)/(m+1)) spans all regions. Exponential R(10) with θ=100h → 0.905.
- Estimation: ML (L=maximize); unbiasedness, MSE, Bessel correction; exponential θ̂=x̄; CIs (z, t, χ² for θ); Type 1 vs Type 2 tests.
- Bayesian: posterior ∝ e^(−λΣtᵢ)λⁿ·prior; sequential updating; propagates distributions through the tree.

## 10. Data (Table XI-1, WASH-1400)

Motors: 1×10⁻³/D fail-to-start, 1×10⁻⁵/hr fail-to-run (1×10⁻³ extreme). Relays 3×10⁻⁶–1×10⁻⁵/hr; switches 1×10⁻⁴/D; breakers 3×10⁻⁶/D; pipe >3″ rupture 1×10⁻⁶–3×10⁻⁵/hr (high-quality 10⁻¹⁰–10⁻⁷); diesel 3×10⁻²/D start, 3×10⁻³/hr run; batteries 1×10⁻⁶/hr; plug valves 1×10⁻³/D. Precision is order-of-magnitude only. Human error appears as normal tree inputs ("operator miscalibrated all sensors" = common cause).

## 11. Pressure tank example (Ch. VIII)

System: pump, 60s fill, pressure switch P, S1/K1 latch, timer relay shutdown. Top: "rupture of pressure tank after pumping start." Construction steps 1–9 (OR over primary/secondary/command; INHIBIT "pump runs >60s ⇒ rupture"; No Miracles; state-of-system chain to K2). Reduced: T = K2 + S·S1 + S·K1 + S·R + T(tank primary, circle). Data: T=5×10⁻⁶, K2=3×10⁻⁵, S=1×10⁻⁴, K1=3×10⁻⁵, R=1×10⁻⁴, S1=3×10⁻⁵ → P(E₁)≈3.4×10⁻⁵; K2 importance 86%, tank 14%. Lessons: duplicate the relay; the system monitors *controls*, not pressure → relief valve + remove timer; AND-gates high near treetop.

## 12. Three motor example (Ch. IX)

60-s test loop for 3 motors via power box, 60-s test signal; relays K1–K7, timers KT1–KT3, batteries. E₁=E₂·E₃, E₂=K5+E₄, E₃=K2+E₅, E₄=K₃·E₆, E₅=K1+KT2·KT3+S1, E₆=K1+E₇+S1, E₇=KT1+KT2+KT3. MCS motor-2 overrun: K5·K2, K5·K1, K5·KT2·KT3? (KT2·KT3), K5·S1, K3·K1, K3·KT1·KT2·KT3, K3·S1 (OCR-ambiguous — verify from source figures IX-4 to IX-10 if exact sets needed). E₅/E₆ differ only in the when-condition → never merge. Extended: wiring faults, "motor 1 fails to start" tree.

## 13. Inductive methods overview (Ch. II)

Parts Count (2×10⁻³ vs true 1×10⁻⁶ for redundant amplifiers), FMEA/FMECA (dual valves: 4×10⁻⁴ per phase → 8×10⁻⁴), Double Failure Matrix (fuel valve configurations), success path enumeration, PHA/FHA. Monthly maintenance downtime example: 1/720 ≈ 1.4×10⁻³ ≫ 10⁻⁶ hardware — "best maintenance policy may be none".

## OCR fidelity notes

"10~3"-style exponents, rotated figure pages (111, 124, 126–127), and equation noise present; interpreted from context. Terms NOT in this handbook: Esary–Proschan, signematics, "DTC continue switch"; MOCUS = cut-set enumeration only. 
