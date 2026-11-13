---
name: Best Model
description: Use when the user asks which model to use, wants better performance, speed, cost, or quality, is unsure about model choice, or complains a task is slow or expensive. Recommends the best available model for the task and explains how to switch. Does not change the active model automatically.
---

# Best Model Selector

## Core principle
A skill cannot change the active model on its own. This skill **recommends** the best available model for the task and tells the user exactly how to switch. Switching mid-session is done with `/models` (or by editing `model` in `opencode.json(c)`).

## Step 0: Clarify the task profile
Ask (or infer) these in ONE short message if missing:
1. Task type: coding/editing, debugging, reasoning/planning, review, docs, or quick Q&A?
2. Priority: quality, speed, or cost (free)?
3. Need vision/multimodal or very long context?
4. Current model (check config or ask) and what's wrong with it?

If the user already gave enough, skip to Step 1.

## Step 1: List available models
Run `opencode models` (CLI) or use the `opencode.models` tool to see what's actually available. Never invent model IDs. Only recommend models that appear in that list.

## Step 2: Pick by task profile

Use this heuristic matrix (prefer models present in the list):

| Task profile | Prefer | Avoid |
|---|---|---|
| Deep reasoning, architecture, complex debugging | Strongest "pro"/reasoning model available (e.g. `google/gemini-2.5-pro`, `gemini-3.1-pro-preview`, or any `*-pro*`) | Flash/lite models |
| Routine coding, edits, refactors | Fast flash model (`gemini-2.5-flash`, `gemini-3.x-flash`) | Heavy pro models (slow/costly) |
| Speed/cost sensitive, disposable tasks | Free `opencode/*-free` models (deepseek, glm, mimo, nemotron, flint, crouton, pulse, beam) | Paid pro models |
| Vision/multimodal input | A gemini pro/flash model (vision-capable family) | Text-only small models |
| Very long context | Pro model with large context window | Small flash models |
| Trivial Q&A | Cheapest/fastest available | Switching at all |

Rules:
- If the task is trivial, **recommend staying on the current model** — switching has overhead and the gain is nil.
- Prefer the *current* model if it already fits the profile (don't switch for marginal gain).
- Never recommend a model not present in the available list.
- Free `opencode/*` models are good defaults for cost; paid `google/*-pro*` for hard reasoning.

## Step 3: Recommend and explain
Output:
- **Recommended model:** `provider/model`
- **Why:** 1-2 sentences tied to the task profile.
- **Trade-offs:** speed/cost/quality note.
- **How to switch:** "Run `/models`, select X" or "set `\"model\": \"X\"` in `opencode.jsonc`".
- **Fallback:** if X unavailable, use Y.

## Step 4: Verify (optional)
After the user switches, confirm with `opencode models` or by checking the status bar. If performance doesn't improve, rerun this skill with the new bottleneck.

## Limitations
- Cannot auto-switch the active model. OpenCode selects the model from config/`/models`; this skill only advises.
- Capabilities are inferred from model family names; verify against the provider's docs for edge cases.
- Switching models mid-conversation resets some context efficiency; prefer deciding up front.

## Red flags
- Don't invent model IDs or capabilities.
- Don't switch models for trivial tasks.
- Don't recommend a paid model when a free one fits.
