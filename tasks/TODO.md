# tasks/todo.md
Task Log (Auditable)

This file tracks active work in small, verifiable increments.
Keep exactly one item "IN PROGRESS" at a time.
Each non-trivial task should end with a Results + Verification Story section.

---

## Working Notes (short-lived)
Keep this section small. Capture only:
- key constraints / invariants
- key decisions (with links to ADR if created)
- pitfalls discovered
- commands used for verification

---

## Backlog (untriaged)
- [ ] (Add items as they arise; move one item to Planned when you start)

---

## Planned (ready to start)
> Move exactly one item from Backlog → Planned → In Progress

### Template (copy for new work)
- [ ] **Goal:** …
- [ ] **Acceptance criteria:** …
- [ ] **Scope:** in / out …
- [ ] **Plan:**
  - [ ] Locate existing patterns / helpers
  - [ ] Implement smallest safe slice
  - [ ] Add/adjust tests
  - [ ] Verify (lint/tests/build/manual)
  - [ ] Summarize results + verification story

---

## IN PROGRESS (exactly one)
> Put the active checklist here

---

## Done (recent)
> Keep last ~5 tasks; archive older if desired
