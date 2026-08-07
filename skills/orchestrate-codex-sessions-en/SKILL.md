---
name: orchestrate-codex-sessions-en
description: "Orchestrate implementation, orchestration complete: coordinate Codex primary tasks, in-thread subagents, visible independent tasks, AGENTS.md contracts, Core/UI/Package/QA stages, Repair loops, and evidence gates from first principles. Use when the user says ‘orchestrate implementation’ or ‘orchestration complete’, or requests multi-session or multi-agent work, parallel subagent scouting, project orchestration, responsibility splitting, long-running handoffs, independent QA, or recoverable development workflows. Do not trigger implicitly for small single-file edits, one-shot answers, or work with no splitting benefit unless the user explicitly invokes this Skill."
---

# Codex Multi-Session Orchestration

Complete the task with the smallest sufficient work units. Use subagents for short-lived information questions and visible independent tasks for durable delivery ownership. Do not treat splitting work as quality by itself.

## Follow the authority order

1. Follow the user's current goal, authorization, and prohibitions.
2. Read and follow the applicable `AGENTS.md`; when it conflicts with this Skill, `AGENTS.md` wins.
3. Follow the available tools, concurrency limits, approval rules, and lifecycle constraints. Do not assume a thread, subagent, wait, or worktree capability exists.
4. Use this Skill's defaults only when the first three layers do not decide the issue.

If visible-task creation, subagents, wait, or worktree support is unavailable, state the boundary and complete the smallest safe portion that remains. Never fabricate delegation or acceptance evidence.

## Choose the work unit first

Answer these questions before splitting work:

1. What must the user ultimately see, and what evidence proves completion?
2. Which state must survive across turns, and which findings are disposable scouting results?
3. Who owns changes, and which files or systems are off limits?
4. Which work is truly independent, and which work depends on an interface or artifact?
5. Does the user need to enter a work unit later to question, redirect, or resume it?

Choose the lowest viable level:

| Level | Structure | Use when |
|---|---|---|
| Level 0 | Primary task completes the work directly | Scope is concentrated, ownership is singular, and handoff adds little value |
| Level 1 | Primary task plus in-thread subagents | Independent search, cross-file tracing, research, or verification can be compressed into evidence |
| Level 2 | Visible primary task plus visible delivery tasks and necessary subagents | Work crosses modules or time, users need direct intervention, or stable ownership or independent QA is required |

Start at Level 0. Upgrade only when evidence shows a higher level is useful.

## Make authorization boundaries explicit

- Create visible tasks or sessions only when the user explicitly requests creation, splitting, or multiple visible tasks. A request to “implement using multi-session orchestration” grants that authority.
- When the user asks only for a plan, comparison, or recommendation, stop at read-only analysis and an orchestration proposal. Do not create visible tasks or modify the project.
- Once the user explicitly authorizes implementation, continue within the established local scope without repeatedly asking for the same permission.
- External writes, publishing, pushing, permission changes, destructive actions, and material scope expansion still require separate authorization.

## Execute the workflow

### 1. Establish the real boundary

- Confirm the real project root, current checkout or worktree, applicable rules, and existing changes.
- Personally read foundational documents and the exact code you will modify in full. Do not delegate either category.
- Turn the final visible result, data definitions, privacy, network, permission boundaries, and required evidence into Acceptance criteria.
- Surface material ambiguity and its consequences. If a minimal safe default exists, state the assumption and continue.

### 2. Draw the dependency and ownership graph

- Split by delivery interface and risk boundary, not by file count.
- For every visible task, define `Owns`, `Must not edit`, prerequisites, deliverables, verification commands, and completion criteria.
- Serialize interface dependencies such as Core → UI → Package/QA.
- Parallelize only independent read-only scouting when current rules allow it.
- A visible task is not file isolation. Serialize overlapping writes in a shared checkout. Parallel writes require non-overlapping ownership or separate worktrees.

### 3. Decide whether to create `AGENTS.md`

- Do not create `AGENTS.md` for Level 0 or a one-off read-only subagent merely for formality.
- Before Level 2, create or update the project-level `AGENTS.md` with product boundaries, ownership, prohibitions, gates, verification, and final Acceptance.
- Preserve existing user rules and add only the minimum project contract required.
- Read [templates.md](references/templates.md) when a template is needed.

### 4. Dispatch subagents

- Dispatch only concrete, independent, well-bounded scouting or verification questions.
- Keep subagents read-only by default. Do not give them code ownership or final design authority unless the user or applicable rules explicitly allow it.
- Make every task brief self-contained with search scope, exact question, and output format. Require `file:line`, symbol names, essential excerpts, or source links.
- Dispatch independent questions in parallel only when current rules allow it, then follow the tool's required wait behavior.
- Treat subagent conclusions as compressed leads. Spot-check cited locations without rereading the entire delegated scope.
- Promote work to a visible task when it requires multiple user decisions, durable modification, or independent acceptance.

### 5. Dispatch visible delivery tasks

- Write self-contained task briefs. Do not assume a new task inherits all primary-task history.
- Include the project path, upstream state, ownership, prohibited scope, Acceptance, verification commands, and required completion report.
- In full orchestrator mode, keep the primary task focused on management, decisions, and acceptance. Do not concurrently edit business code already owned by a delegated task.
- After each implementation task completes, verify scope, interfaces, check results, and downstream usability before starting dependent work.

### 6. Monitor and enforce gates

- Prefer wait or snapshot capabilities for visible tasks. Avoid noisy high-frequency polling.
- Report only meaningful milestones, decisions, blockers, gate results, and repair closure.
- A task's self-declared completion is not acceptance. Check actual changes, command output, artifacts, and unverified items.
- Preserve raw environment errors. Never use shims, `0 tests`, permission bypasses, or prose inference to manufacture a green result.
- Read [gates-and-evidence.md](references/gates-and-evidence.md) when full gates are required.

### 7. Run independent QA and Repair

- Keep QA read-only. Require file or line references, reproduction scenarios, expected behavior, impact, and reasons for anything unverified.
- After confirming a defect, create the smallest Repair task for each independent root cause. Do not let QA fix defects opportunistically.
- Limit Repair to the authorized scope, leave the smallest regression check, and return the result to the original QA task for verification.
- Record toolchain and permission blockers as environment boundaries, not as product passes or product defects.

### 8. Deliver the final result

Report separately:

- user-visible artifacts and entry points;
- actual modification scope;
- self-check, test, Debug, Release, and packaging results;
- independent cross-checks against real data or external facts;
- visible UI and runtime state;
- security, privacy, network, permission, and publishing boundaries;
- unverified items, causes, and impact.

Do not substitute “build succeeded” for “the user can see it.” Do not substitute “the process exists” for “the interaction was verified.”

## Stop condition

Stop after all authorized scope is complete and the evidence chain is closed. If completion requires a new business choice, external coordination, destructive action, or scope expansion, report the completed portion and the single blocking decision, then wait for the user.
