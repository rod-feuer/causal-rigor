# Framework Check — Five Logic Lenses

## What this does
Audits a framework, taxonomy, model, or category system in a piece of writing for structural logical
errors that panels built for other jobs (causal, copywriting, PMM) won't catch. The five most
common failure modes: a category that implies dependencies it hasn't earned, an implicit "all"
where the evidence supports only "some," buckets that leak or overlap, hidden premises doing
load-bearing work without being stated, and framing that telegraphs structural inferences the
author didn't intend.

Use before publishing any piece that introduces a taxonomy, model, or named set of categories.
The causal panel catches X→Y errors; this catches "the framework implies X is always/only/
exhaustively Y" errors.

## The five
| # | Lens | Tradition | The question it asks |
|---|------|-----------|----------------------|
| 1 | Aristotle | Definitional consistency / category theory | "Is the term defined consistently? Does each example fit the definition — or does the definition drift as it's applied?" |
| 2 | Barbara Minto | MECE — Mutually Exclusive, Collectively Exhaustive | "Are the categories actually clean: no overlap, no gap? Does the framing imply exhaustiveness it hasn't earned?" |
| 3 | Karl Popper | Scope and falsifiability | "Are there implicit universal claims ('all X are Y') where only 'some X I found were Y' is supported? What would it look like if the framework were wrong?" |
| 4 | Ludwig Wittgenstein | Ordinary-language precision | "Does the term mean what the author thinks it means to a first-time reader? Where does the author's technical sense drift from the reader's natural reading?" |
| 5 | George Lakoff | Framing — unintended structural inferences | "What structural relationships does the wording activate that weren't intended? What does a reader infer about dependency, sequence, or completeness that the text didn't explicitly claim?" |

## Evaluation protocol
1. **State the framework** — the taxonomy, model, or category system being introduced. Name the
   categories and the relationship claimed between them. Decompose compound frameworks into
   individual claims.
2. **Run each lens INDEPENDENTLY** — for each: **Diagnosis** (what the lens reveals) · **Verdict**
   (clean / scope-error / definitional-drift / MECE-violation / hidden-premise / framing-overreach)
   · **The fix** (the minimal rewrite that corrects it, or confirmation that it's clean).
3. **Synthesize** — **What's structurally clean** · **What needs correction** (ranked by severity) ·
   **Single most important fix** · **Minimal rewrite** (concrete new words, not advice).
4. **Blind spots** — this panel checks logical structure, not causal identification
   (→ `causal-panel-eval`), persuasiveness (→ `copywriting-panel-eval`), or positioning
   (→ `pmm-panel-eval`). It does not check whether the framework is *true* — only whether it's
   *logically consistent with what's claimed*.

## Output format
```
## [Framework under test]
### Lens Assessments — [per lens: Diagnosis / Verdict / Fix]
### Synthesis — Structurally clean / Needs correction / Most important fix / Minimal rewrite
### Blind Spots
```

## Framework references

### 1. Aristotle — Definitional consistency / category theory
**Concept:** A category is defined by necessary and sufficient conditions. An example either fits
the definition or it doesn't. Definition drift is the failure mode: the word starts meaning one
thing and quietly shifts to mean another within the same piece. The classic test: substitute the
definition for the term everywhere it appears — does the sentence still mean the same thing?
**Diagnostics:** Is the term defined (explicitly or implicitly)? Does the definition hold across
all uses? Does each example satisfy the definition — or is the author relying on reader charity?
Is the category sharp enough to exclude things?

### 2. Barbara Minto — MECE
**Works:** *The Pyramid Principle*. **Concept:** Categories should be **Mutually Exclusive** (no
item belongs to two) and **Collectively Exhaustive** (the categories cover all cases). Implied
MECE is the specific risk in public writing: the author doesn't claim exhaustiveness but a neat
list of three implies it.
**Diagnostics:** Can an item belong to two categories simultaneously? Does the framing imply
"these are all the cases" when it isn't? Are there obvious items that fall outside all categories?
Is the ME/CE status of the framework stated or just implied?

### 3. Karl Popper — Scope and falsifiability
**Works:** *The Logic of Scientific Discovery*; *Conjectures and Refutations*. **Concept:** The
scope of a claim should match the evidence: "all X are Y" requires universal support; "some X I
found were Y" is honest when that's what you have. Implicit universals are the failure mode:
"Pile 3 claims are frontier calls" sounds definitional but may only describe the observed sample.
**Diagnostics:** Is the claim scoped to the evidence, or does it reach beyond it? Are there
implicit "always," "all," "every," "never" that haven't been earned? What would it look like if
the framework were wrong — is that scenario ruled out, or just not mentioned?

### 4. Ludwig Wittgenstein — Ordinary-language precision
**Works:** *Philosophical Investigations*. **Concept:** Meaning is use. The risk in technical
frameworks is that the author assigns a precise meaning to a common word ("frontier," "alpha,"
"judgment") and relies on readers to track the technical sense throughout. Language drift is the
failure mode: the author uses the word technically; the reader hears it ordinarily.
**Diagnostics:** Does the author's use of a term match the first-time reader's natural reading?
Where does the technical definition diverge from ordinary usage? Is the special meaning
established clearly enough to survive to the end of the piece?

### 5. George Lakoff — Framing / unintended structural inferences
**Works:** *Metaphors We Live By*; *Don't Think of an Elephant*. **Concept:** Framing activates
structural relationships in the reader's mind below the level of explicit claim. "Under each
overconfident headline" activates a containment frame: Pile 3 is *inside* Pile 2. "Which leads
us to Pile 3" activates a sequence frame: Pile 3 follows necessarily from Pile 2. These
inferences are picked up automatically — and they can be wrong without any explicit claim being
false.
**Diagnostics:** What structural relationships (containment, sequence, causation, exhaustiveness)
does the wording activate? Are those relationships actually claimed — or just implied? Would a
reader infer a dependency, ordering, or completeness that the framework doesn't assert?

## Selection guide
- *I'm publishing a piece with a named framework or taxonomy* → all five lenses.
- *Is my definition consistent throughout?* → Aristotle + Wittgenstein.
- *Did I overclaim scope?* → Popper + Minto.
- *Does the wording imply something I didn't mean?* → Lakoff + Wittgenstein.
- *Are my categories clean and complete?* → Minto + Aristotle.

## Interaction notes & cross-refs
- **Founding case (2026-06-28):** The Pile 2→Pile 3 link in a LinkedIn post implied all Pile 3
  claims come from under Pile 2 overconfident headlines. Lakoff catches the containment/sequence
  framing; Popper flags the implicit universal. Neither the causal panel nor the copywriting
  panel caught it — correct, because neither is scoped for structural/definitional errors.
- **Chain:** framework-check (logical structure) → causal-panel-eval (causal identification) →
  pmm-panel-eval (positioning) → copywriting-panel-eval (the words).
- This panel checks logical consistency, not truth. A framework can pass all five lenses and
  still be wrong — causal and epistemics panels handle that.
- Provenance: built 2026-06-28 to catch the structural/definitional error class that the causal
  panel (X→Y identification) is not designed for.
