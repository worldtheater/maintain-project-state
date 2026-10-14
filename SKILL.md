---
name: maintain-project-state
description: Maintain a concise, evidence-backed project snapshot for orientation, handoff, and resumption across coding-agent sessions. Read it without mutation for status questions; reconcile or update it only when the user or repository instructions authorize maintenance.
---

# Maintain Project State

Maintain one compact projection of the project's current reality so another session can continue without reconstructing the repository or depending on conversation history. Source code, tests, logs, protocol fixtures, and accepted design documents remain authoritative; the state file is a derived navigation and handoff artifact.

Use with coding agents that can read project files and inspect Git. Updating state also requires write access to the selected state file.

## Locate and assess the state

1. Resolve the user's project root, preferring the Git root.
2. Use a user- or project-specified path; otherwise use `.codex/project-state.md` at that root. This configurable path convention can be shared by different agents; keep one state file rather than creating a separate copy per tool.
3. Read the state before investigating broadly. Do not rewrite it merely because it was read.
4. In a Git repository, inspect the current root, branch or worktree, and `git status --short`. If the state is meant to travel between checkouts or machines, verify that it is tracked.
5. If the state is tracked, find its latest commit and inspect the commits and changed paths from that commit to `HEAD`, plus dirty changes. Treat recorded verification as evidence from the state snapshot, not automatically as evidence for a newer `HEAD`.
6. Follow changed paths and existing source pointers only as far as the current request requires. Current evidence wins over stale state.

If the file is absent, create it only when initialization or maintenance is authorized. Otherwise report that no maintained snapshot exists and continue from repository evidence.

## Choose the operation

### Orient

Use for status questions, planning, resumption, and handoff review.

- Distinguish state-derived context from facts verified in the current session.
- Verify only claims relevant to the requested work.
- Do not mutate the state unless the user or repository instructions authorize maintenance.

### Update

Use when material evidence changes project purpose, architecture, ownership, protocol, storage, project-specific conventions, delivery state, risks, decisions, active work, or meaningful verification boundaries.

- Patch the current projection; never append a session log.
- Replace superseded facts, remove resolved items, and preserve unaffected accurate content.
- Record implementation status, verification limits, and uncommitted changes separately; use the closure rules below to decide what is still in progress.
- Update before a requested commit so the state travels with the change. Do not commit, amend, or push unless separately authorized.

### Handoff

Use when the user asks to pause, hand off, switch threads or accounts, or continue material active work elsewhere.

- If `In Progress` is already sufficient, do not rewrite it.
- Otherwise record at most one compact bullet per active objective: the goal, current evidence or key paths, the next action or decision, and the validation or blocker that still matters.
- Mention a branch or worktree only when continuation depends on that non-default checkout.
- Do not create a parallel handoff document or copy conversation history into the state.
- If continuation will use another checkout or machine, state whether required work is still uncommitted. The state file cannot transfer dirty files, local logs, credentials, or account-specific configuration; do not commit or push them without authorization.

## Close work when it is done

On every authorized state update, reconcile the entire `In Progress` section before adding the current work; do not re-investigate every old implementation.

- Keep an item only when a concrete next action is still requested or required to finish its agreed scope. Name that action and the evidence or blocker; age, a dirty file, and an old `[active]` label are not reasons to retain it.
- Use current evidence and the user's completion/acceptance statement to close work. A commit is evidence of delivery, not proof of correctness or acceptance. If contradictory evidence shows a material defect, retain that specific defect rather than the whole finished task.
- Separate implementation, verification, and Git status. Implemented work may be uncommitted or partially verified; say so without automatically labeling it active. Required unfinished validation remains active; optional or unspecified manual QA belongs in one concise `Verification` boundary, not an evergreen task.
- On completion, remove the active entry in the same update. Merge only lasting capability or constraint changes into the existing `Implemented`/architecture bullet; omit minor fixes. Do not move the full task narrative to another section or an archive document.
- Superseded work is replaced, canceled work is removed, and explicitly paused work is labeled paused with only the evidence and resume condition needed. Do not invent a new backlog from old acceptance caveats or resume paused work automatically.
- If an old item's status is uncertain, check its narrow source/commit pointer. Ask only when the uncertainty materially affects continuation; never silently mark unfinished work complete merely to meet the item limit.

## State shape

```markdown
# Project State

## Purpose and Boundaries
- ...

## Current Architecture
- ...

## Project Conventions
- ...

## Implementation State
### Implemented
- ...
### In Progress
- [active] Goal: ... Evidence: `path` / symbol. Next: ... Validation or blocker: ...
### Next
- ...

## Known Problems and Risks
- P1 [confirmed|risk]: ... Evidence: `path` / symbol.

## Open Decisions
- D1: ... Impact: ...

## Verification
- ...

## Source Pointers
- `path` — why it is useful or authoritative.
```

Keep the standard headings predictable. Omit empty problem and decision entries. Adapt labels to the project's language without changing their meaning.

## Keep it compact and trustworthy

- Target about 3,000 tokens; treat 4,000 as the default hard limit.
- Keep architecture to 10 bullets, project conventions to 8, implemented capabilities to 8, in-progress and next work to 3 each, risks to 7, open decisions to 5, and verification boundaries to 5.
- Write the current state, not chronology. Let Git retain history. Keep each active objective to one short paragraph with source pointers; remove obsolete “this commit/session” wording and per-run test/build narratives instead of appending updates.
- Keep one fact per bullet and point to stable paths, symbols, or headings instead of copying implementation detail.
- Keep one managed copy of project-specific conventions. Do not duplicate them across state, root instructions, and subsystem instructions.
- Separate implemented, verified, planned, inferred, and unknown claims. Never turn design intent into implementation fact.
- Do not store secrets, account-specific settings, or absolute machine-local paths. Record capability or setup requirements without sensitive values when they affect continuation.
- Remove stale or duplicated material before exceeding the hard limit; ask before deliberately retaining more.

Prioritize active continuity, architectural invariants, confirmed risks and decisions, major delivered capabilities, then verification boundaries and source pointers.

## Repository entrypoint

When the repository adopts this workflow:

- Keep the project's agent instruction file (for example, root `AGENTS.md`) as a minimal bootstrap pointing to this skill and the state path. Use the instruction-file convention recognized by the host agent.
- Include a short fallback telling a session without the skill to read the state and reconcile it against Git before working.
- Keep the actual project facts and conventions in the state, retaining nested instruction files only for genuinely local rules.
- Do not create, rewrite, or remove instruction files unless the user authorized that repository-level change.

## Finish maintenance

Before reporting completion:

1. Re-read the state as if no conversation history were available.
2. Check every `In Progress` item has a remaining scoped action; close completed/superseded entries and remove resolved risks. Do not retain a task solely for missing optional manual QA.
3. Check the whole document's item and size budgets, including `Implemented` and `Verification`; compact stale, repeated, and overly detailed content before finishing. Distinguish historical verification from current-session validation.
4. Check the diff and, when portability matters, confirm that the state and repository-owned skill are intended to be tracked.
5. Report what changed and any claims left uncertain or unverified.
