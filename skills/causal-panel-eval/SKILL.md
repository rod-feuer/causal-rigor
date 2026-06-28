---
name: causal-panel-eval
description: >-
  Pressure-test a CAUSAL claim — "X drove/caused/leads to Y," "doing X produces Y," "the metric
  moved because of Z," "this intervention works" — for identification: does the evidence actually
  support causation, or only association dressed as cause? Five causal-inference lenses (Pearl —
  graphical models / ladder of causation; Rubin — potential outcomes / counterfactuals; Heckman —
  selection bias; Cartwright — causal pluralism & external validity; Bradford Hill — association→
  causation criteria). Use whenever a claim asserts cause/effect, "drives," "because," a result is
  attributed to an action, an A/B or experiment is interpreted, or you suspect correlation-as-
  causation (the most common form of fake rigor in business). Complement to epistemics-panel-eval
  (is the measurement valid?) — this asks: even if measured well, does X actually CAUSE Y?
---

# Causal Panel — Five Causal-Inference Lenses

## What this does
Pressure-tests a causal claim through five independent lenses from the people who built modern
causal inference. The recurring job: separate **what's causally supported** from **what's a
plausible story** — confounding, reverse causation, selection, construct→cause leaps, and
external-validity overreach. Correlation-dressed-as-causation is the single most common form of
*performed rigor* in business (a confident chart + a real number + a narrative, with no
identification). This panel is the tool that catches it. It does NOT judge whether the thing was
measured well (→ `epistemics-panel-eval`) or framed well (→ `pmm-panel-eval`).

## The five
| # | Lens | Tradition | The question it asks |
|---|------|-----------|----------------------|
| 1 | Judea Pearl | Graphical models / do-calculus / ladder of causation | "Which rung — association, intervention, or counterfactual? Draw the DAG: what confounders and colliders sit between X and Y, and is the effect *identified*?" |
| 2 | Donald Rubin | Potential outcomes | "What's the counterfactual (Y if not-X)? How was treatment assigned — is assignment ignorable, or entangled with the outcome?" |
| 3 | James Heckman | Selection bias | "Is the sample selected on something tied to the outcome? Are you looking at survivors / a non-random slice?" |
| 4 | Nancy Cartwright | Causal pluralism / external validity | "It worked *here* — will it travel *there*? 'No causes in, no causes out': what causal assumptions are smuggled in? Do the support conditions hold elsewhere?" |
| 5 | Austin Bradford Hill | Association→causation criteria | "When a clean experiment is impossible: strength, consistency, temporality, dose-response, plausibility, coherence, specificity — how many hold?" |

## Evaluation protocol
1. **State the causal claim** — the asserted **cause → effect**, and the evidence offered. Decompose compound claims into separate cause→effect statements (most "findings" smuggle several). If vague, ask.
2. **Run each lens INDEPENDENTLY** — for each: **Diagnosis** · **Verdict** (identified / association-only / confounded / selection-biased / reverse-or-common-cause / mechanism-underdetermined / external-validity-overreach) · **Sharpening** (the design that would identify it, or the narrower claim the evidence actually supports). Pearl and Rubin are the identification core; Cartwright is the generalization check; run all three hard.
3. **Synthesize** — **What's causally supported** vs **what's storytelling** · the **confounders/alternatives** not ruled out · **the claim that survives** (rewrite it to exactly what the evidence licenses) · the cheapest design that would upgrade it.
4. **Blind spots** — measurement validity (→ `epistemics-panel-eval`), positioning (→ `pmm-panel-eval`), and the fact that this panel reasons about identification — it does not run the experiment.

## Output format
```
## [Causal claim(s) under test]
### Lens Assessments — [per lens: Diagnosis / Verdict / Sharpening]
### Synthesis — Causally supported vs storytelling / Unruled-out alternatives / The claim that survives / Cheapest upgrade
```

## Framework references

### 1. Judea Pearl — graphical causal models, do-calculus, ladder of causation
**Concept:** Three rungs — **association** (seeing: P(Y|X)), **intervention** (doing: P(Y|do(X))), **counterfactual** (imagining: would Y have happened without X). You cannot climb from association to intervention without causal assumptions, usually a **DAG**. Confounders (common causes of X and Y) bias the estimate; **colliders** (common effects) create spurious association if conditioned on. **Diagnostics:** Which rung does the evidence actually sit on? Draw the DAG — what's the back-door path? Is the effect identified, or is a confounder doing the work? Any collider being conditioned on (the classic "controlling for X created the correlation" trap)?

### 2. Donald Rubin — potential outcomes / counterfactual framework
**Concept:** Each unit has potential outcomes under treatment and control; the causal effect is their difference; the "fundamental problem" is you only observe one. Causal inference = principled guessing of the missing counterfactual. Clean only when **treatment assignment is ignorable** (independent of potential outcomes) — true in RCTs, suspect in observational data. **Diagnostics:** What is the counterfactual here, concretely? How was treatment assigned — randomized, self-selected, or confounded? Is there a credible control, or a before/after with everything else changing too?

### 3. James Heckman — selection bias
**Concept:** When units enter the sample (or the treatment) based on factors related to the outcome, naive comparisons are biased. Survivorship is the popular-business form. **Diagnostics:** Is the sample non-random in a way tied to Y? Are failures excluded (survivorship)? Did subjects self-select into treatment? Is the "winners did X" inference ignoring the winners-who-didn't and losers-who-did?

### 4. Nancy Cartwright — causal pluralism, external validity, "no causes in, no causes out"
**Concept:** Even a clean local result (X caused Y *here*) need not generalize — it holds only where the **support factors** (the rest of the causal structure) also hold. "No causes in, no causes out": you can't derive a causal conclusion without causal premises. RCTs establish *that* it worked somewhere, not *that it will work here*. **Diagnostics:** What support conditions did the result depend on? Will they hold in the target context? What causal assumptions are being smuggled as if they were data?

### 5. Austin Bradford Hill — association→causation viewpoints
**Concept:** When randomization is impossible, weigh pragmatic considerations: **strength, consistency, temporality (cause precedes effect), biological/mechanistic plausibility, coherence, dose-response, specificity, experiment, analogy.** Not a checklist to tick — a structured way to judge whether association is plausibly causal. **Diagnostics:** Is temporality even right (or could it be reverse)? How many viewpoints hold? Is "plausibility" being used to wave through an unidentified effect?

## Selection guide
- *Did our action actually drive the metric?* → Rubin + Pearl + Heckman.
- *Will what worked in the pilot work at scale / elsewhere?* → Cartwright + Heckman.
- *Is this "X causes Y" claim from observational data legit?* → Pearl + Hill + Heckman.
- *Is this just correlation in a confident costume?* → all five.

## Interaction notes & cross-refs
- A null result is the trap Pearl + Rubin catch best: "no effect, *because* the cause was already present" is usually **underdetermined** — many causal stories fit one null. Don't infer a mechanism from an absence.
- Construct→cause leaps (n=1 of a category, attributed to the category) are Heckman/Rubin territory — the manipulated thing is rarely the named construct.
- Chain: **strategy** (`eight-strategist-eval`) → **measurement soundness** (`epistemics-panel-eval`) → **causal identification** (this) → **positioning** (`pmm-panel-eval`) → **words** (`copywriting-panel-eval`).
- Provenance: built 2026-06-21 to audit the de-biasing finding's causal claims before they were used as a public receipt — separating the one supported claim (the intervention shifted output) from three causal overreaches (null-mechanism, construct-level overshoot, delta-as-construct).
