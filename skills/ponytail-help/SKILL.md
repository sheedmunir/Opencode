---
name: ponytail-help
description: >
  Quick reference for ponytail levels, companion skills and deactivation.
  One-shot display. Use for /ponytail-help, "ponytail help",
  "how do I use ponytail".
---

# Ponytail Help

Display this reference card when invoked. One-shot: do NOT change mode, write
files, or persist anything.

## Levels

| Level | Trigger | What changes |
|-------|---------|--------------|
| **Lite** | `/ponytail lite` | Build what was asked, name the smaller option in one line. |
| **Full** | `/ponytail` | Smallest complete change, a check where the logic needs one, and a reply naming what was skipped and any risk. Default. |
| **Ultra** | `/ponytail ultra` | Also questions the request and pushes back before building. |

The level sticks until changed or the session ends.

## Skills

| Skill | Trigger | What it does |
|-------|---------|--------------|
| **ponytail** | `/ponytail` | The doctrine itself: least new code, surgical diffs, verified results, clear replies. |
| **ponytail-review** | `/ponytail-review` | Quality review of a diff: bugs, security, load, missing tests, speed, what to cut. Each finding says what goes wrong and how to fix it. |
| **ponytail-audit** | `/ponytail-audit` | The same review for a whole repo, ranked. |
| **ponytail-debt** | `/ponytail-debt` | Harvest `shortcut:` comments into a ledger. |
| **ponytail-gain** | `/ponytail-gain` | Provenance card for the published impact figures. |
| **ponytail-help** | `/ponytail-help` | This card. |

## Deactivate

Say "stop ponytail" or "normal mode". Resume anytime with `/ponytail`.
`/ponytail off` also works.

## Boundaries

These skills report and advise; they do not change code unless the user asks.
