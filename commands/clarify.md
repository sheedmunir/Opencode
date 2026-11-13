---
description: Plan a coding task and clarify requirements. Does not write code until I say "go code."
---


Do not write, edit, or run any code until I explicitly say "go code."

Your job right now is to clarify the task, not to build it.

1. Read the README and any AGENTS.md or docs in the project first, and summarize the conventions you found, so you don't contradict them.
2. Check the relevant project files. Mention any existing code or dependencies that affect the plan. Skip questions you can answer from those files.
3. Restate the goal in one or two sentences, so I can confirm you understood it.
4. Ask the questions that would change the design, one at a time, and say why each matters. Use the interactive question tool with 2 to 4 options where possible, instead of listing them as plain text.
5. Only plan what I asked for. Flag extra features as suggestions, and keep them out of the plan.
6. List every assumption you're making, so I can correct any that are wrong.
7. List the features, the files you expect to touch, the tech stack you'd use, and the main risks or unknowns.
8. Flag any input handling, login, or data storage that needs care, and say how you'll handle it.
9. Prefer the simplest approach that works, and explain why any extra complexity is needed.
10. Note how the layout will behave on phones and small screens.
11. Propose a plan in numbered steps. For each step, name the test you'll write, such as a Playwright test for user flows, and note whether it can be committed on its own.
12. End with a checklist of what must be true for the task to count as finished.
13. Keep a short list of open questions you couldn't resolve. Don't guess at answers.
14. Keep your responses short. Don't re-read files you've already read in this session. If the session gets long, tell me before continuing.
15. Stop and wait to clear any clarifications needed. Do not start coding until I reply "go code."  or use the /go-code command

Task: $ARGUMENTS
