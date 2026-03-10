# AGENTS - Global Guidelines

This file is the single source of truth for global agent behavior. Repo-specific rules live in each repo's AGENTS.override.md (if present) or AGENTS.md, and should be loaded after this file.

## Start Here

### Reading Order (fast path)
1. **Global AGENTS.md** (this file) – global rules and skills.
2. **Repo AGENTS.override.md** if it exists; otherwise **Repo AGENTS.md**.
3. **Repo README.md** – setup and commands.

## Core Rules (Non-Negotiable)

- Principles to follow: DRY, SOLID, YAGNI, KISS, no over engineering, no useless abstraction.
- Do not commit secrets or local config files (.env, tokens, private keys, auth.json, etc.).
- Fail fast on missing required config (no silent defaults).
- No speculative abstractions; keep changes minimal and aligned to existing patterns.
- Don't edit existing migrations; add new ones for schema changes.
- Avoid drive-by dependency upgrades; keep lockfile changes scoped and justified.
- No behavior changes without tests (or explicit justification).
- Avoid cross-surface refactors (backend + frontend + infra) unless required.
- After fixing the root problem, remove leftover scaffolding/temporary edits.

## Default mode

Unless the user explicitly requests implementation or file changes,
operate in read-only mode.

Read-only mode means:
- Explain, analyze, or propose approaches
- Reference existing code by reading it
- Create plans if asked
- Do not modify, create, or delete files

If intent is unclear, ask for clarification before making changes.

## Escalation heuristics

Default to the lightest valid workflow.

### Stay in light mode when:
- The task is explanatory or advisory
- Changes are confined to 1–2 files
- The change is low risk and localized
- The request is clearly specified

### Suggest `create-plan` when:
- More than 2–3 files are likely to change
- The task spans multiple steps or concerns
- Requirements or scope are partially unclear
- A coordinated test or rollout is needed

### Pause and ask for confirmation when:
- The request implies cross-surface changes (e.g., backend + frontend)
- The change may affect production behavior or data
- The task involves migrations, auth, or security-sensitive logic

### Never auto-escalate:
- Do not introduce heavy workflows or additional documentation
- Do not create plan files unless explicitly requested or required
- Do not switch personas to “Coder” unless implementation is explicitly requested

## Instruction priority (conflict resolution)

When multiple skills or rules apply, resolve conflicts using the following priority order.
Higher tiers override lower tiers.

### Tier 1 — Safety, scope, and correctness (highest priority)
These rules must always be followed, even if they conflict with other instructions.

- light-task-runner
- env-config
- security-related rules
- “Do not implement unless explicitly asked”
- “Deliver exactly what the user requested”

### Tier 2 — Execution discipline
These rules govern *how* work is done once execution is allowed.

- workflow
- agents / personas (Architect, Planner, Coder, Tester, Reviewer, etc.)
- testing requirements
- PR discipline
- rollout / rollback expectations

Personas influence reasoning style and focus only.
They must never override Tier 1 rules.

### Tier 3 — Style, conventions, and philosophy (lowest priority)
These rules guide consistency but must yield to higher tiers if needed.

- coding-conventions
- development-principles
- naming/style preferences
- documentation style rules

If two rules conflict:
- Always follow the higher-tier rule.
- If conflict remains within the same tier, ask the user before proceeding.


## Detailed Rules (Skills)

For specific tasks, load the relevant context from `$CODEX_HOME/skills/`.
Do not guess—consult the skill file first.

Always load the **agents** skill when doing actual work (planning, implementation, reviews, or testing) to apply the required persona behavior.
Ignore repo-local skills unless explicitly requested by the user, except when a repo-local skill is clearly necessary for safe or correct changes (e.g., legacy guardrails or localization rules).

| Task Context              | Required Skill File                            |
| :------------------------ | :--------------------------------------------- |
| **Planning / Starting**   | `$CODEX_HOME/skills/create-plan`               |
| **Workflow / Execution**  | `$CODEX_HOME/skills/workflow`                  |
| **Agents / Personas**     | `$CODEX_HOME/skills/agents`                    |
| **Development Principles**| `$CODEX_HOME/skills/development-principles`    |
| **Coding Conventions**    | `$CODEX_HOME/skills/coding-conventions`        |
| **Testing**               | `$CODEX_HOME/skills/testing`                   |
| **Env / Config**          | `$CODEX_HOME/skills/env-config`                |
| **Light Task Runner**     | `$CODEX_HOME/skills/light-task-runner`         |
| **WSL Test Runner**       | `$CODEX_HOME/skills/wsl-test-runner`           |
