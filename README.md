# causal-rigor

A three-rung system for catching and correcting causal reasoning errors in Claude Code sessions. Built to separate *what's causally supported* from *what's a plausible story* — the most common form of performed rigor in business and content.

Each rung is independent. Install one, some, or all.

---

## Rung 1 — The nudge (`CLAUDE.md`)

An in-pass behavioral rule. On any claim that asserts cause — "X drove Y," "because of Z," a result attributed to an action — Claude names the counterfactual, the top confounder, and whether the claim is *identified* or only *consistent-with* the evidence before agreeing or moving on.

"Well-identified" is a valid verdict. The goal is calibration, not manufactured doubt.

**Install:** Copy `CLAUDE.md` into your project root (or merge Rule 17 into an existing `CLAUDE.md`). For machine-wide coverage, copy it to `~/.claude/CLAUDE.md`.

---

## Rung 2 — The hook (`.claude/hooks/causal-check.sh`)

An automated Stop hook. When Claude's final response contains causal-attribution language (`caused`, `drove`, `led to`, `resulted in`, `due to`, etc.), it re-injects a forced second pass:

1. Counterfactual — what happens without the asserted cause?
2. Confounder — the single most plausible alternative explanation not ruled out
3. Verdict — IDENTIFIED, or only CONSISTENT-WITH?

Loop-guarded. Silent when nothing load-bearing matches — "Causal check: clean" is an expected, valid outcome.

**Install:**

```bash
# Copy the hook
mkdir -p ~/.claude/hooks
cp .claude/hooks/causal-check.sh ~/.claude/hooks/causal-check.sh
chmod +x ~/.claude/hooks/causal-check.sh
```

Then add the Stop block to `~/.claude/settings.json`:

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "/Users/YOUR_USERNAME/.claude/hooks/causal-check.sh",
            "timeout": 10
          }
        ]
      }
    ]
  }
}
```

For project-level only (not machine-wide): the hook and `.claude/settings.json` in this repo are already wired up — just clone and open in Claude Code.

**Tuning:** Edit the `pattern=` line in the script to tighten or loosen triggers. **Disable:** Remove the Stop block from `settings.json`, or toggle via `/hooks`.

---

## Rung 3 — The causal skill (`skills/causal-panel-eval/SKILL.md`)

An on-demand deep audit via five causal-inference lenses: Pearl (graphical models / DAG), Rubin (potential outcomes), Heckman (selection bias), Cartwright (external validity), Bradford Hill (association→causation criteria).

Use when a claim is load-bearing — being wrong is expensive. Invoke with `/causal-panel-eval` or reference the skill in your prompt.

**Install:**

```bash
mkdir -p ~/.claude/skills/causal-panel-eval
cp skills/causal-panel-eval/SKILL.md ~/.claude/skills/causal-panel-eval/SKILL.md
```

---

## Rung 4 — The framework skill (`skills/framework-check/SKILL.md`)

An on-demand audit via five logic lenses: Aristotle (definitional consistency), Minto (MECE — mutually exclusive / collectively exhaustive), Popper (scope and implicit universals), Wittgenstein (ordinary-language drift), Lakoff (unintended framing inferences).

Use when publishing a piece that introduces a taxonomy, model, or named set of categories. Catches the structural/definitional error class that the causal panel isn't designed for — e.g. a category that implies dependencies it hasn't earned, or framing that telegraphs a structural relationship the author didn't intend. Invoke with `/framework-check`.

**Install:**

```bash
mkdir -p ~/.claude/skills/framework-check
cp skills/framework-check/SKILL.md ~/.claude/skills/framework-check/SKILL.md
```

---

## The ladder

| Rung | What it is | When it fires | Cost |
|------|-----------|---------------|------|
| 1 — Nudge | CLAUDE.md rule | Every turn with a causal claim | Zero — in-pass |
| 2 — Hook | Stop hook | Automatically on session end | Near-zero — shell script |
| 3 — Causal skill | Five-lens causal panel | On demand | One LLM call |
| 4 — Framework skill | Five-lens logic panel | On demand | One LLM call |

Rung 1+2 catch most cases cheaply. Rungs 3+4 are for claims and frameworks where being wrong matters.

---

## Honest caveats

- The hook re-examines Claude's own output (role-flipped second pass), not a fully independent critic. That's most of the benefit cheaply. For true independence, swap the script's `jq` block for a `claude -p "refute the causal claims in: <text>"` call.
- The settings watcher may not pick up a new hook mid-session. If it doesn't fire, open `/hooks` once to reload config.
- "Causal check: clean" is a valid, expected outcome. The system is not designed to manufacture doubt.
