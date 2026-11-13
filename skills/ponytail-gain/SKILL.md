---
name: ponytail-gain
description: >
  Provenance card for the published impact figures behind this skill,
  with the caveat that they are upstream benchmark averages, not this repo's.
  One-shot display. Use for /ponytail-gain, "what does ponytail save",
  "ponytail impact".
---

# Ponytail Gain

Display this card when invoked. One-shot: do NOT change mode, write files, or
persist anything.

These ponytail were merged from an upstream "lazy senior dev" skill family that
published one agentic benchmark. The figures below are that benchmark's, reproduced
here for provenance — not measurements of this repo or of your current session.

## Scoreboard

Render plain ASCII bars. Bar length is a share of the no-skill baseline; the label
carries the exact figure.

```
  upstream benchmark       39 tasks × 5 runs · 5 runs each

  no-skill        ████████████████████  100%
  Lines of code   █████████···········   47%   ▼ 53%
  Output tokens   ███████████·········   55%   ▼ 45%
  Cost            ███████████████·····   74%   ▼ 26%
  Time            ████████████········   59%   ▼ 41%
  Hidden checks passed   97%  (no-skill 96%)
  Tests where the logic needs one   98%  (no-skill 68%)

  This repo:  /ponytail-debt  (shortcuts you deferred)
              /ponytail-audit (what's still cuttable)
```

## Honesty boundary

These are upstream averages, not this repo. NEVER print a per-repo savings number
("you saved X lines/tokens here"): the unbuilt version was never written, so there
is no real baseline to subtract from in a live repo. The only real per-repo figures
come from `/ponytail-debt` (a counted ledger); point there instead of inventing one.

## Boundaries

One-shot display. Edits nothing, changes no mode.
