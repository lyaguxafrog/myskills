---
name: recall
description: Поиск ранее накопленного опыта и проектных знаний
compatibility: opencode, claude, codex
---

# Recall Skill

## Purpose

The `recall` skill is used whenever the agent encounters uncertainty, a failure, an unexpected result, or a technical obstacle.

Its purpose is to search previously accumulated project knowledge before attempting new investigation.

The skill acts as the project's memory retrieval mechanism.

Use it before:

* Extensive debugging.
* Trial-and-error experimentation.
* Architectural changes.
* Infrastructure modifications.
* Dependency upgrades.
* Refactoring decisions.
* Repeated investigation of known problems.

The goal is to avoid solving the same problem twice.

---

# Trigger Conditions

Run `recall` when any of the following occur:

* Build failure.
* Test failure.
* CI failure.
* Deployment failure.
* Unexpected runtime behavior.
* Infrastructure issue.
* Authentication issue.
* Network issue.
* Performance regression.
* Tooling problem.
* Missing project context.
* Unclear architectural decision.
* Unknown command or workflow.
* Repeated error message.

Do not immediately start debugging.

First attempt knowledge retrieval.

---

# Core Principle

Past experience is usually cheaper than new investigation.

Always search existing knowledge before creating new knowledge.

Priority order:

1. Existing project documentation.
2. ADRs and architecture notes.
3. AGENTS.md.
4. Previous Dream records.
5. Changelog history.
6. Repository conventions.
7. New investigation.

---

# Execution Flow

## Phase 1 — Define The Problem

Create a concise problem statement.

Include:

### Problem

What is failing?

### Context

Where did it happen?

### Symptoms

Observed behavior.

### Expected Behavior

What should happen instead?

### Impact

How severe is the issue?

---

## Phase 2 — Search Project Knowledge

Search all available project memory.

Potential sources:

* AGENTS.md
* README.md
* docs/*
* architecture/*
* deployment/*
* development/*
* ADRs
* CHANGELOG.md
* Previous Dream entries
* Project memory files

Look for:

* Similar failures.
* Similar implementations.
* Related architectural decisions.
* Known limitations.
* Existing workarounds.
* Required workflows.
* Previously solved incidents.

---

## Phase 3 — Search Dreams Collection

Using Anytype MCP:

### Target

* Space: <Resolved Space Name>
* Collection: Dreams

## Space Resolution

Before accessing Anytype, determine the target space.

Resolution order:

1. Read SPACE.md located in the same directory as this skill.
2. Use the contents as the Anytype space name.
3. If SPACE.md does not exist, ask the user for the space name.
4. Never assume a default space.

The space name resolved from SPACE.md becomes the target for all Anytype operations.

Search for entries related to:

* Similar errors.
* Similar technologies.
* Similar integrations.
* Similar infrastructure.
* Similar symptoms.

Extract:

* Root causes.
* Fixes.
* Lessons learned.
* Risks.
* Workarounds.

---

## Phase 4 — Build Knowledge Summary

Create a concise summary.

### Relevant Knowledge Found

* ...

### Similar Incidents

* ...

### Previous Resolutions

* ...

### Known Risks

* ...

### Recommended Direction

* ...

---

## Phase 5 — Decide Next Action

If sufficient knowledge exists:

### Reuse Existing Knowledge

Follow the previously documented solution.

Avoid duplicate investigation.

If partial knowledge exists:

### Extend Existing Knowledge

Start investigation from the known information.

Do not restart from scratch.

If no knowledge exists:

### New Investigation Required

Proceed with debugging.

Mark the issue as a candidate for future Dream preservation.

---

## Phase 6 — Confidence Assessment

Estimate confidence level.

### High Confidence

The issue closely matches a known case.

### Medium Confidence

Partial overlap exists.

### Low Confidence

No useful prior knowledge found.

---

## Output Format

Recall Summary

### Problem

* ...

### Sources Consulted

* ...

### Relevant Knowledge Found

* ...

### Similar Incidents

* ...

### Recommended Actions

* ...

### Confidence

* High
* Medium
* Low

### New Investigation Needed

* Yes
* No

---

# Knowledge Usage Rules

When prior knowledge exists:

* Prefer documented solutions.
* Prefer ADR decisions.
* Prefer project conventions.
* Prefer previous Dream entries.

Do not ignore established project knowledge without justification.

If a documented solution is rejected:

Record why.

---

# Success Criteria

After running `recall`, the agent should know:

* Whether the problem has already been solved before.
* Which documentation is relevant.
* Which architectural decisions apply.
* Which previous lessons are relevant.
* Whether new investigation is actually necessary.

The agent should never begin a major investigation without first attempting recall.

