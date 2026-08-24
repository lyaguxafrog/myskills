---
name: afk
description: dsf
compatibility: claude, codex, pi, opencode
license: MIT
---

# Away From Keyboard

## Purpose

Enable autonomous execution while the user is temporarily unavailable.

When this skill is active, the agent should continue working without interrupting the user for clarifications whenever possible. Instead, the agent should make decisions according to the selected autonomy level, record those decisions, and provide a summary at the end.

This skill is intended for situations where waiting for user input would unnecessarily block progress.

---

## Activation

Examples:

```text
Use Away From Keyboard: lite
Use Away From Keyboard: normal
Use Away From Keyboard: full
```

or

```text
/afk lite
/afk normal
/afk full
```

---

## Core Principle

When a question arises during execution:

1. Determine whether the decision is allowed by the current autonomy level.
2. If allowed:

   * Make the decision.
   * Record the reasoning.
   * Continue working.
3. If not allowed:

   * Stop and ask the user.

The objective is to maximize forward progress while remaining within the granted authority.

---

# Autonomy Levels

## Lite

Low-risk decisions only.

Allowed examples:

* Naming variables, functions, files, and modules.
* Formatting and linting fixes.
* Small refactoring with unchanged behavior.
* Choosing obvious defaults.
* Minor documentation improvements.
* Reorganizing code without architectural impact.

Not allowed:

* Architectural changes.
* Public API changes.
* Database schema changes.
* Security-sensitive decisions.
* Infrastructure changes.
* Business logic modifications.

Decision guideline:

> If a reasonable engineer would consider the change cosmetic or routine, it is likely allowed.

---

## Normal

Medium-risk decisions are allowed.

Includes everything from Lite plus:

* Choosing implementation approaches.
* Selecting libraries or frameworks.
* Modifying internal APIs.
* Restructuring components.
* Creating new modules or services.
* Adjusting CI/CD workflows.
* Making design trade-offs.

Not allowed:

* Destructive actions.
* Large-scale migrations.
* Security policy changes.
* Financially impactful actions.
* Irreversible operations.

Decision guideline:

> Prioritize the option most likely to achieve the user's stated goal with minimal complexity.

---

## Full

Maximum autonomy.

The agent is authorized to make all technical decisions necessary to complete the task.

Includes everything from Normal plus:

* Architectural decisions.
* Major refactors.
* Data migrations.
* Public API redesign.
* Strategic implementation trade-offs.
* Requirement interpretation when ambiguity exists.

Restrictions:

* Do not violate explicit user instructions.
* Do not knowingly cause data loss.
* Do not perform external financial, legal, or contractual actions.
* Do not bypass security controls without a compelling reason.

Decision guideline:

> Act as the responsible technical owner of the task.

---

# Decision Framework

Whenever multiple options exist:

1. Identify available options.
2. Evaluate risks and benefits.
3. Select the option that best advances the user's goals.
4. Record the decision.
5. Continue execution.

Do not stop merely because multiple valid solutions exist.

---

# Decision Log

For every autonomous decision, record:

```yaml
decision:
  title: Storage backend selection
  level: normal
  options:
    - PostgreSQL
    - Redis
  selected: Redis
  rationale: Existing architecture already depends on Redis and latency requirements favor in-memory storage.
```

Keep entries concise.

---

# End-of-Task Summary

At the conclusion of work, provide:

```markdown
# AFK Summary

Mode: Normal

Decisions Made: 3

## Storage Backend
Selected: Redis

Reason:
Existing infrastructure already includes Redis.

---

## Authentication Method
Selected: OIDC

Reason:
Matches existing identity provider.

---

## Project Structure
Selected: Feature-based layout

Reason:
Improves maintainability as the codebase grows.
```

The summary should contain only meaningful decisions, not trivial implementation details.

---

# Escalation Rules

The agent must stop and request user input when:

* A decision exceeds the current autonomy level.
* Multiple options have significantly different business outcomes.
* Requirements are fundamentally contradictory.
* The requested action appears unsafe or potentially destructive.
* The task requires information unavailable to the agent.

When uncertain:

* Lite → ask.
* Normal → prefer asking.
* Full → prefer deciding.

---

# Success Criteria

The skill is successful when:

* User interruptions are minimized.
* Progress continues despite ambiguity.
* Decisions remain traceable.
* The final summary explains what was decided and why.
* The user can quickly review the autonomous choices made during execution.
