# Heavy Work Orchestrator (Opt-In)

## Purpose

This document defines a strict, audit-grade workflow for **large, high-risk, or regulated** engineering tasks.

It is **not active by default** and must be explicitly requested.

---

## Activation rules

This workflow applies **only** when one of the following is true:

- The user explicitly requests it (e.g. “use the heavy orchestrator”)
- The user confirms after a suggestion for strict/audit-grade execution

If not explicitly activated, this document must be ignored.

---

## Relationship to other rules

When active:

- This workflow **temporarily overrides**:
  - `light-task-runner`
  - escalation heuristics
  - default minimal execution flow
- It **does not override**:
  - Tier 1 safety and scope rules
  - “Do not implement unless explicitly asked”

After completion, control returns to the default workflow.

---

## Core principles

- Correctness > speed
- Evidence > confidence
- Explicit decisions > implicit assumptions
- No skipped steps
- No speculative work

---

## Required artifacts (only for this mode)

Create and maintain the following **only while this workflow is active**:

- `requirements.md` — user requirements and constraints
- `plan.md` — step-by-step execution plan
- `design.md` — architecture and tradeoffs
- `verification.md` — tests, commands, and evidence

Do not create these files outside of this workflow.

---

## Workflow phases

### Phase 0 — Instruction audit

- Identify all instruction sources:
  - system instructions
  - repo `AGENTS.md`
  - any task-specific documents
- Record conflicts and resolutions in `verification.md`
- Ask the user if conflicts cannot be resolved safely

---

### Phase 1 — Requirements

- Extract requirements exactly as stated
- List constraints and non-goals
- Identify blocking unknowns
- Stop and ask if correctness is blocked

Deliverable: `requirements.md`

---

### Phase 2 — Plan (with task tracker)

- Create a clear, ordered execution plan
- Represent the plan as a checklist with checkboxes
- Each checkbox must correspond to a meaningful unit of work
- Keep the checklist coarse-grained (no micro-steps)

The checklist in `plan.md` is the **authoritative task tracker**.

Rules:
- Check an item only when it is fully complete
- Do not auto-check remaining items
- Leave incomplete items unchecked if work is paused

Deliverable: `plan.md`


---

### Phase 3 — Design

- Document 2–3 viable approaches
- Analyze tradeoffs (risk, complexity, maintenance)
- Select one approach with justification

Deliverable: `design.md`

---

### Phase 4 — Implementation

- Re-read all artifacts before coding
- Implement incrementally
- Keep changes targeted
- Stop and ask if new ambiguity appears
- Follow the plan in order
- After completing a checklist item, update its checkbox in `plan.md`
- Only update a checkbox when the work is fully complete and verified
- Do not modify the plan structure unless requirements change

---

### Phase 5 — Verification (mandatory)

Define success **before** declaring completion.

Include:

- Tests run (exact commands + results)
- Observable behavior
- Exit codes or concrete outputs

Deliverable: `verification.md`

No task is complete without evidence.

---

## Completion checklist

Before declaring the work done:

- All requirements are met
- All tests pass
- Evidence is recorded
- No unexplained assumptions remain
- Rollback considerations are documented (if applicable)
- All checklist items in `plan.md` are checked
  OR remaining unchecked items are explicitly documented as out of scope

---

## Exit condition

After completion:

- Do not continue using this workflow
- Return to the default light execution model
