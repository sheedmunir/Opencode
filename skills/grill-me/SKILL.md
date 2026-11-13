---
name: grill-me
description: A relentless, critical interview to interrogate and sharpen a proposed plan, architecture, or design before implementation. Use when the user wants their ideas pressure-tested, asks to be "grilled", or asks for a rigorous stress test of a technical design.
---

# Grill-Me (Plan & Design Stress Test)

Conduct a rigorous, constructive interrogation of the user's plan or design. The goal is to surface hidden assumptions, unhandled edge cases, security holes, and execution bottlenecks before a single line of code is written.

## Process

1. **Intake the Proposal**:
   - Ask the user to share the plan, architectural design, or feature spec if not already provided.
   - Clarify the core goal, non-negotiables, and technical constraints.

2. **The Interrogation Loop**:
   - Focus on one critical vulnerability at a time. Do not overwhelm with 20 questions at once—ask 2 to 3 targeted, high-leverage questions per turn.
   - Drill into:
     - **Failure modes**: What happens when the network fails, dependencies timeout, or inputs are malformed?
     - **Scalability & State**: Where is state kept? How are race conditions prevented?
     - **Complexity**: Is this over-engineered? What is the simplest thing that could work?
     - **Trade-offs**: What is being sacrificed (speed vs simplicity vs maintainability)?

3. **No Flattery**:
   - Do not validate weak arguments or give unearned agreement.
   - Push back when requirements are vague or hand-wavy ("we'll handle caching later").

4. **Synthesis**:
   - Once all key areas have been stress-tested, summarize the hardened plan with clear mitigations for the risks surfaced during the grilling.
