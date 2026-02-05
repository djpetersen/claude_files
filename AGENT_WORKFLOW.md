# AGENT_WORKFLOW.md
AI Coding Agent Runbook

This file defines how work is planned, executed, verified, and documented.
Claude must also follow the reasoning and scope rules in CLAUDE.md.
If there is a conflict, CLAUDE.md takes precedence.

---

## 1. Plan Mode Default

Enter Plan Mode for any non-trivial work:
- 3+ steps
- multi-file changes
- architectural decisions
- production-impacting behavior

In Plan Mode:
- clarify requirements
- identify files to touch
- define acceptance criteria
- include verification steps in the plan

If new information invalidates the plan:
**stop, update the plan, then continue.**

When requirements are unclear:
write a crisp spec (inputs, outputs, edge cases, success criteria).

---

## 2. Subagent Strategy (Parallelize Intelligently)

Use subagents to keep main context clean and parallelize safely.

Good subagent tasks:
- repo exploration
- pattern discovery
- test failure triage
- dependency or API research
- risk review

Rules:
- One focused objective per subagent.
- One concrete deliverable.
- Synthesize outputs into a short actionable summary before coding.

---

## 3. Incremental Delivery (Reduce Risk)

Prefer thin vertical slices over big-bang changes.

Workflow:
implement → test → verify → expand

When feasible:
- ship behind feature flags
- use config switches or safe defaults

Do not mix refactors with behavior changes unless required for safety.

---

## 4. Task Management (Auditable)

### Files
- `tasks/todo.md` — plans, checklists, progress
- `tasks/lessons.md` — failure modes and prevention rules

### Plan First
For non-trivial work, write a checklist in `tasks/todo.md`:
- implementation steps
- verification steps
- acceptance criteria

### Track Progress
- One “in progress” item at a time.
- Mark items complete as you go.

### Document Results
At completion, add:
- what changed
- where
- how it was verified

---

## 5. Verification Before “Done” (Non-Negotiable)

Never mark complete without evidence.

### Verification Story (Required)
Include:
- what commands were run (tests/lint/build)
- what passed
- what was not run and why
- how to reproduce manually if applicable

If verification was skipped:
provide exact commands the user can run.

Ask:
“Would a staff engineer approve this diff *and* the verification story?”

---

## 6. Decision Records (ADR-Lite)

For non-trivial design, schema, or architectural decisions:
- Record a short decision note (inline or in `docs/adr/`):
  - context
  - decision
  - alternatives considered
  - consequences

Avoid re-litigating decisions without new information.

---

## 7. Self-Improvement Loop

After any user correction or discovered mistake:
add an entry to `tasks/lessons.md`:
- failure mode
- detection signal
- prevention rule

Review `tasks/lessons.md`:
- at session start
- before major refactors

---

## 8. Autonomous Bug Fixing (With Guardrails)

When given a bug:
reproduce → isolate root cause → fix → add regression coverage → verify

Do not offload debugging to the user unless blocked.

If blocked:
- ask exactly one targeted question
- provide a recommended default
- explain what changes based on the answer

---

## 9. Communication Guidelines (User-Facing)

- Lead with outcome and impact.
- Reference concrete artifacts (files, commands, errors).
- Avoid narrating every step.
- Summarize logs; do not dump them.
- State assumptions and constraints explicitly.
- Always include the verification story.

---

## 10. Error Handling & Recovery

### Stop-the-Line Rule
If something unexpected happens:
- stop adding features
- preserve evidence
- return to diagnosis and re-plan

### Safe Fallbacks
Prefer safe defaults + warnings over partial behavior.
Avoid broad refactors under time pressure.

### Rollback Strategy
For risky changes:
- keep changes reversible
- use flags or disabled-by-default configs

---

## Definition of Done

A task is done when:
- behavior matches acceptance criteria
- verification has passed (or is explicitly documented)
- risky changes have rollback strategies
- code follows existing conventions
- readability meets the bar
- a short verification story exists
