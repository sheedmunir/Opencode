---
name: project-memory
description: Use when user wants to persist project progress in docs/PROJECT.md, record where the project is going and where work stopped, capture described future features, project-specific features and constraints, and list unsolved errors or blockers for later resume. Triggers on save progress, document project, where did we leave off, resume later, update project memory, create or update PROJECT.md, project state, or at end of a milestone/feature/fix.
---

# Project Memory

Keeps the project's living memory in `docs/PROJECT.md` so work can be resumed without re-reading the whole conversation.

## Core principle

Evidence before claims. The file records only what is verified from code, git, logs, and the conversation. Unknowns stay marked `Unknown` — never fill them with plausible invention.

## When to use

- User says: **save progress**, **document project**, **where did we leave off**, **resume later**, **create/update PROJECT.md**, **project state**
- Auto-save: after completing a milestone, feature, bugfix, or design decision — update the file before replying, unless user says not to

## File

Path: `docs/PROJECT.md` in the project root. Create `docs/` if missing.

## Template — use this exact shape

```markdown
# PROJECT.md — <Project Name>

Updated: YYYY-MM-DD
Status: <one-line current state>

## 1. Where we are
- Done: <verified completed work, with file paths>
- Evidence: <command / commit / test output that proves it>

## 2. Where we are going
- Next: <concrete next step>
- Direction: <why / goal>

## 3. Features described, not yet implemented
- <feature name>: <short description of intended behavior>
- (keep empty with "None" if none)

## 4. Project-specific features and constraints
- <quirk / constraint / device limit>: <fact>
- Paths, ports, channels, gateways, build commands

## 5. Unsolved errors and blockers
- <error>: <symptom> — <repro steps> — <logs / command output> — <hypotheses>
- (keep empty with "None" if none)

## 6. Decisions
- <decision>: <why>

## 7. How to resume
1. <first command to run>
2. <where to look>
```

## Workflow

1. Read evidence first: `git status` / `git log --oneline -5`, relevant source files, recent error output. Do not rely on conversation memory alone.
2. Read existing `docs/PROJECT.md` if present — update in place, never rewrite from scratch to erase history.
3. Write the file. Keep each bullet one line. Total under 120 lines — this is a state card, not a design doc or ADR collection.
4. Mark gaps as `Unknown — needs <what>` instead of guessing.
5. After writing, reply with: "Saved to `docs/PROJECT.md` — <one line of current status>." plus the next step from section 7.

## Example

User: *"Save progress for the Extender web page. Future controls planned, wl0.1 channel error unsolved."*

`docs/PROJECT.md`:

```markdown
# PROJECT.md — Extender Web Page

Updated: 2026-11-07
Status: Design agreed, no code written yet (waiting for GO CODE)

## 1. Where we are
- Done: Flow agreed — busybox httpd (option A), page password only, page stays ON after extend
- Evidence: `Ext/extender.sh` reviewed; design discussion 2026-11-07

## 2. Where we are going
- Next: Implement web extender on user signal "GO CODE"
- Direction: Daily dashboard — status, reconnect, change uplink, change Ext names

## 3. Features described, not yet implemented
- Dashboard controls: status, reconnect, delete saved, change uplink + password, change Ext/Ext5G names, stop extender

## 4. Project-specific features and constraints
- Runs inside shell/extender mode only; firmware web server not running then
- wl0 is uplink client, wl0.1 is 2.4G AP (shared channel), wl1 is 5G AP; br0 gateway IP

## 5. Unsolved errors and blockers
- wl0.1 2.4G appears only after uplink known (channel shared) — workaround: stage Ext5G first, rebuild Ext fresh after uplink chosen

## 6. Decisions
- BusyBox httpd: lightest fit for router vs pure-shell server or Python/Node
- Page password only, Ext/Ext5G stay open

## 7. How to resume
1. `cd Ext && sh -n extender.sh`
2. Wait for GO CODE before writing code
```

## Common mistakes

- Inventing a roadmap, test results, or log lines not seen in the repo → verify first, or mark `Unknown`
- One-off narrative ("first we tried X...") → keep decisions only, drop journey
- Updating only "where we are" → always update all 7 sections so future resume has full context
