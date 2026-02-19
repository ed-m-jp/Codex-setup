---
name: create-plan
description: Create a concise plan. Use when a user explicitly asks for a plan related to a coding task.
metadata:
  short-description: Create a plan
---

# Create Plan

## Goal

Create a clear, actionable plan and only write plan files when explicitly required by the repo or user.

## Planning Rules

- Always use the todo tool before starting any task touching more than 2 files.
- Ensure "Run linter" and "Run tests" are always the final two items in any TODO list.

## Minimal workflow

1. **Read-only until approval**
   - Operate in read-only mode while drafting the plan.
   - If the repo or user requires a plan file (e.g. PLAN.md), only write it **after** the plan is validated.

2. **Scan context quickly**
   - Read `README.md` and any obvious docs (`docs/`, `CONTRIBUTING.md`, `ARCHITECTURE.md`).
   - Skim relevant files (the ones most likely touched).
   - Identify constraints (language, frameworks, CI/test commands, deployment shape).

3. **Ask follow-ups only if blocking**
   - Ask **at most 1–2 questions**.
   - Only ask if you cannot responsibly plan without the answer; prefer multiple-choice.
   - If unsure but not blocked, make a reasonable assumption and proceed.

4. **Create a plan using the template below**
   - Start with **1 short paragraph** describing the intent and approach.
   - Clearly call out what is **in scope** and what is **not in scope** in short.
   - Then provide a **small checklist** of action items (default 6–10 items).
     - Each checklist item should be a concrete action and, when helpful, mention files/commands.
     - **Make items atomic and ordered**: discovery → changes → tests → rollout.
     - **Verb-first**: “Add…”, “Refactor…”, “Verify…”, “Ship…”.
   - Include at least one item for **tests/validation** and one for **edge cases/risk** when applicable.
   - If there are unknowns, include a tiny **Open questions** section (max 3).

5. **After approval (if required)**
   - Write the validated plan to the repo’s `PLAN.md` (or equivalent).
   - Update the plan checkboxes as work progresses.

6. **After completion (if required)**
   - Remove `PLAN.md` once the work is done, unless the repo explicitly says to keep it.

7. **Do not preface the plan with meta explanations; output only the plan as per template**

## Plan template (follow exactly)

```markdown
# Plan

<1–3 sentences: what we’re doing, why, and the high-level approach.>

## Scope

- In:
- Out:

## Action items

[ ] <Step 1>
[ ] <Step 2>
[ ] <Step 3>
[ ] <Step 4>
[ ] <Step 5>
[ ] <Step 6>

## Open questions

- <Question 1>
- <Question 2>
- <Question 3>
```

## Checklist item guidance

Good checklist items:

- Point to likely files/modules: src/..., app/..., services/...
- Name concrete validation: “Run npm test”, “Add unit tests for X”
- Include safe rollout when relevant: feature flag, migration plan, rollback note

Avoid:

- Vague steps (“handle backend”, “do auth”)
- Too many micro-steps
- Writing code snippets (keep the plan implementation-agnostic)
