---
description: Build an approved plan from /clarify. Use only after I say "go code."
---

Only start now because I said "go code." Follow the approved plan from the clarify step. If no plan was approved in this session, stop and ask me to run /clarify first.

If any part of the approved plan is ambiguous or has an open question, stop and ask me before writing any code. Do not guess.

Work in this order:

1. Use the ponytail skill to write the simplest code that meets each step of the plan.
2. Use the ponytail-review skill to review the code you wrote.
3. Use the verification-before-completion skill before saying any step is done, and confirm each item on the finished checklist.
4. Use the webapp-testing skill with Playwright to write and run tests for each user flow. If a test fails, fix the code, not the test.

Design step: if the task involves visual or UI design, stop before writing any UI code and ask me which design skill to use. Show me the design-related skills you have available, with one line on what each does, and wait for my choice before continuing.

Security: never hardcode secrets, API keys, or passwords. Validate and escape all user input. Don't commit .env files. Run a dependency check before finishing, and flag any package you add.

Commit each completed step separately, and report what passed and what failed.

Keep your responses short, and don't re-read files you've already read in this session.

Task: $ARGUMENTS
