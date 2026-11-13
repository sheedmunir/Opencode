# Error-Type Triage Reference

Read this when a fix stalls at the first triage step, or when you need the
per-class checklist. It complements `SKILL.md`'s loop-first process; it is not
a replacement for it.

## The Stop-the-Line Rule

When anything unexpected happens:

```
1. STOP adding features or making changes
2. PRESERVE evidence (error output, logs, repro steps)
3. DIAGNOSE using the triage checklist
4. FIX the root cause
5. GUARD against recurrence
6. RESUME only after verification passes
```

Don't push past a failing test or broken build onto the next feature. Errors compound.

## Triage checklist

Work in order; don't skip.

### Step 1: Reproduce

Reproduce with the repository's own test/build commands:

```bash
# Run the specific failing test (substitute the project's own command)
npm test -- --grep "test name"
# Verbose / isolated, to rule out pollution
npm test -- --verbose path/to/test        # --runInBand for Node
```

Can't reproduce? Check timing (timestamps, artificial delays, load), environment
(Node/browser/OS/env vars, empty vs populated data, CI), state (leaked globals,
shared caches, isolation vs full suite) — or document conditions and monitor.

### Step 2: Localize

```
Which layer is failing?
├── UI/Frontend     → console, DOM, network tab
├── API/Backend     → server logs, request/response
├── Database        → queries, schema, data integrity
├── Build tooling   → config, dependencies, environment
├── External service → connectivity, API changes, rate limits
└── Test itself     → is the test wrong? (false negative)
```

Regression bug? Bisect: `git bisect start / bad / good <sha> / git bisect run <test-command>`.

### Step 3: Reduce

Minimal failing case — strip inputs, callers, config, code until removing anything
goes green. A minimal repro makes the root cause plain and prevents symptom-fixing.

### Step 4: Fix the root cause

Symptom ("user list shows duplicates" → dedup in the UI) vs root cause ("the API
JOIN duplicates rows" → fix the query). Ask "why does this happen?" until the cause is yours.

### Step 5: Guard against recurrence

One regression test for this exact failure; it must fail before the fix and pass after.

### Step 6: Verify end-to-end

Specific test → full suite → build → manual spot check.

## Per-class patterns

**Test failure** — Did you change the code the test covers? If yes: outdated test
(update it) or buggy code (fix it). If unrelated: side effect (shared state, imports,
globals). Flaky: timing, order dependence, external deps.

**Build failure** — Type error: read the error at the cited location. Import error:
module exists? exports match? paths correct? Config error: schema/syntax. Dependency:
lockfile/install. Environment: runtime/OS compatibility.

**Runtime error** — null/undefined: trace data flow. Network/CORS: URLs, headers,
server CORS. White screen: error boundary, console, component tree. No error at all:
targeted logs at key points.

## Instrumentation rules

Add logs only when they answer a question the loop can't. Remove them when done;
keep only error boundaries, API error logging with context, key-flow metrics.
Never log secrets or PII.

## Common rationalizations

| Excuse | Reality |
|--------|---------|
| "I know what it is, I'll just fix it" | Right 70% of the time; the rest costs hours. Reproduce first. |
| "The failing test is probably wrong" | Verify. If it's wrong, fix the test — don't skip it. |
| "Works on my machine" | Check CI, config, deps. |
| "Fix it in the next commit" | Next commits will pile bugs on bugs. |
| "Flaky test, ignore it" | Flaky tests mask real bugs. Fix the flake or understand it. |

## Final verification

- [ ] Root cause documented
- [ ] Fix addresses cause, not symptom
- [ ] Regression test exists (fails without fix, passes with)
- [ ] Full suite green; build succeeds
- [ ] Original scenario verified end-to-end
