---
name: dream
description: Рефлексия по окончанию дня
compatibility: opencode, claude, codex
---

# Dream Skill

## Purpose

The `dream` skill is a project reflection and memory-consolidation process executed at the end of a work session.

Its purpose is to transform today's work into durable project knowledge.

The skill should:

1. Understand what happened today.
2. Separate temporary context from long-term knowledge.
3. Preserve architectural decisions.
4. Update project documentation.
5. Record changes for future agents.
6. Reduce knowledge loss between sessions.

Think of this skill as the project's long-term memory formation process.

---

# Core Principle

Not everything learned today deserves to be remembered.

Store only information that will remain useful weeks or months later.

Examples of information worth preserving:

* Architecture decisions.
* Development workflows.
* Build procedures.
* Deployment requirements.
* Infrastructure topology.
* Project conventions.
* Coding standards.
* Testing requirements.
* Security constraints.
* Integration details.
* Known limitations.
* Frequently encountered pitfalls.

Examples of information that should NOT be preserved:

* Temporary debugging logs.
* One-time errors.
* Intermediate experiments.
* Local environment accidents.
* Task management notes.
* Ephemeral TODO lists.

---

# Execution Flow

## Phase 1 — Gather Context

Analyze all available evidence from the current session.

### Source Material

Review:

* Files modified.
* Files created.
* Files removed.
* Commands executed.
* Test executions.
* CI results.
* Build results.
* Errors encountered.
* Bugs fixed.
* Features implemented.
* Refactorings performed.
* Documentation changes.
* Design discussions.
* Architectural discussions.

Determine:

* What changed.
* Why it changed.
* Whether the change is complete.
* Whether future work is required.

---

## Phase 2 — Build Session Timeline

Reconstruct the work chronologically.

For each major activity identify:

### Activity

* What was done.

### Motivation

* Why it was done.

### Outcome

* What was learned.

### Status

* Completed
* Partial
* Blocked
* Abandoned

Do not store the timeline permanently unless it contains durable project knowledge.

Use it only to understand the session.

---

## Phase 3 — Extract Durable Knowledge

Identify new information that future agents would benefit from knowing.

### Architecture

* New components.
* New services.
* New dependencies.
* New integration points.

### Development

* Required commands.
* Build workflows.
* Testing workflows.
* Repository conventions.

### Infrastructure

* Host requirements.
* Container requirements.
* Network assumptions.
* Authentication systems.

### Security

* Authentication mechanisms.
* Authorization rules.
* Secret handling requirements.

### Project Conventions

* Naming rules.
* Directory structure expectations.
* Coding patterns.
* Review requirements.

Only retain information that is likely to remain true.

---

## Phase 4 — Update Documentation

Prefer updating existing documentation.

Search for the most appropriate location before creating new files.

Potential targets:

* AGENTS.md
* README.md
* docs/*
* architecture/*
* deployment/*
* development/*
* ADRs
* CHANGELOG.md

For every documentation update:

1. Verify the information is durable.
2. Avoid duplication.
3. Place information near related content.
4. Improve existing documentation before adding new sections.

---

## Phase 5 — Record Architectural Decisions

For each significant decision identify:

### Decision

What was chosen.

### Context

What problem existed.

### Alternatives

What other options were considered.

### Reasoning

Why the selected approach won.

### Consequences

Expected benefits and trade-offs.

Store in:

* Existing ADR files.
* Architecture notes.
* Project memory files.

If no decision repository exists, recommend creating one instead of inventing a new format.

---

## Phase 6 — Validate Documentation Drift

Compare implementation against documentation.

Look for:

* Undocumented behavior.
* Obsolete documentation.
* Missing setup steps.
* Missing dependency descriptions.
* Missing operational procedures.

Update documentation when discrepancies are discovered.

---

## Phase 7 — Update Changelog

Only if user-visible or developer-visible behavior changed.

Categorize entries under:

### Added

New functionality.

### Changed

Behavior modifications.

### Fixed

Bug fixes.

### Removed

Removed functionality.

Follow the project's existing changelog format.

Do not create releases or version numbers.

---

## Phase 8 — Preserve Engineering Experience (Anytype)

Record noteworthy engineering experience from the session in Anytype.

### Purpose

Preserve practical lessons that may help future engineers and agents avoid repeating mistakes.

Only record information that is likely to remain useful beyond the current session.

### Target

Store records through Anytype MCP.

This step is mandatory.

If MCP access is available, the agent MUST create or update an entry in:

* Space: <Resolved Space Name>
* Collection: Dreams

### What To Record

Record only meaningful engineering experience such as:

* Difficult debugging sessions.
* Unexpected behavior.
* Infrastructure issues.
* Tooling limitations.
* Environment-specific pitfalls.
* CI/CD problems.
* Integration challenges.
* Authentication or networking issues.
* Performance bottlenecks.
* Architectural trade-offs discovered during implementation.

Do NOT record:

* Personal notes.
* Temporary TODO items.
* Routine command execution.
* Trivial mistakes.
* Ephemeral local issues with no future value.

## Space Resolution

Before accessing Anytype, determine the target space.

Resolution order:

1. Read SPACE.md located in the same directory as this skill.
2. Use the contents as the Anytype space name.
3. If SPACE.md does not exist, ask the user for the space name.
4. Never assume a default space.

The space name resolved from SPACE.md becomes the target for all Anytype operations.

### Dream Entry Format

Title:

Session Dream — YYYY-MM-DD

Fields:

#### Project

Project name.

#### Summary

Short description of the session.

#### Challenges Encountered

For each challenge record:

* Problem
* Root Cause
* Resolution
* Lessons Learned

#### Notable Discoveries

Record unexpected findings that improved understanding of:

* Project architecture
* Infrastructure
* Tooling
* Framework behavior
* Third-party integrations

#### Useful Discoveries

Knowledge that future agents should know.

#### Documentation Updates

Documentation modified during the session.

#### Architectural Decisions

References to ADRs or architecture changes.

#### Future Risks

Potential future issues discovered.

### Quality Filter

Before creating an entry ask:

1. Would another engineer benefit from reading this?
2. Is the lesson reusable?
3. Is the information likely to remain useful for at least one month?

If the answer to all three questions is not "yes", do not store it.

### Failure Handling

If MCP, Anytype, Astra space, or Dreams collection is unavailable:

1. Continue the dream process.
2. Mention the failure in the Dream Report.
3. Include the data that should have been stored.
4. Do not silently skip preservation.

---

## Phase 9 — Generate Dream Report

Produce a final report.

### Format

Dream Summary

#### Completed

* ...

#### Learned

* ...

#### Documentation Updated

* ...

#### Architectural Decisions

* ...

#### Project Knowledge Preserved

* ...

#### Documentation Gaps Found

* ...

#### Challenges Encountered

* ...

#### Lessons Learned

* ...

#### Future Work

* ...

#### Risks

* ...

#### Open Questions

* ...

#### Anytype Status

* Entry created successfully in Astra → Dreams

OR

* Failed to create entry (include reason)

---

# Knowledge Preservation Rules

Before storing information ask:

1. Will this still matter in one month?
2. Will another engineer benefit from knowing it?
3. Is it a project fact rather than a task detail?
4. Is it already documented elsewhere?

If any answer is "no", do not preserve it.

---

# Success Criteria

After running `dream`, a new engineer or agent should be able to understand:

* What was accomplished.
* What was learned.
* How the system currently works.
* Important architectural decisions.
* Development and deployment expectations.
* Remaining risks and open questions.
* Important engineering lessons and recurring pitfalls preserved in Anytype (Astra → Dreams).
* What difficulties were encountered and how they were solved.

without needing access to today's conversation.

