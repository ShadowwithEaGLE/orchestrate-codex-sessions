---
name: orchestrate-codex-sessions-en
description: "Use proactively for useful independent subtasks, implementation with independent review, cross-module or cross-source work, deliverable handoffs, or ongoing acceptance. Choose primary work, in-thread subagents, or visible tasks; manage model routing, dependencies, and verification. Skip simple questions and small edits with no delegation benefit unless explicitly invoked."
---

# Codex Multi-Session Orchestration

Complete the task with the smallest sufficient work units. The primary test is whether the full execution trace can be safely discarded after returning a compressed result. Use an in-thread subagent when it can; use a sidebar-visible task when identity, state, handoff, or user intervention must persist. Do not treat splitting work as quality by itself.

**Non-bypassable dispatch gate:** Before calling any delegation tool, including `spawn_agent`, visible-task creation, or fork, output the “Declare routing before dispatch” table. Do not delegate without the table; Level 1 internal agents are not exempt.

## Follow the authority order

1. Follow the user's current goal, authorization, and prohibitions.
2. Read and follow the applicable `AGENTS.md`; when it conflicts with this Skill, `AGENTS.md` wins.
3. Follow the available tools, concurrency limits, approval rules, and lifecycle constraints. Do not assume a thread, subagent, wait, or worktree capability exists.
4. Use this Skill's defaults only when the first three layers do not decide the issue.

If visible-task creation, subagents, wait, or worktree support is unavailable, state the boundary and complete the smallest safe portion that remains. Never fabricate delegation or acceptance evidence.

## Choose the work unit first

Answer these questions before splitting work:

1. What must the user ultimately see, and what evidence proves completion?
2. Can the full execution trace be safely discarded after returning a compressed result?
3. Which state must survive across turns, and which state is disposable?
4. Who owns final delivery, and must the user enter this work unit directly?
5. Does it require an independent project, branch, worktree, formal handoff, or failure recovery?

| Level | Structure | Essence |
|---|---|---|
| Level 0 | Primary task completes the work directly | Work is concentrated and delegation adds little value |
| Level 1 | Primary task plus in-thread subagents | Disposable short-lived delegation; the primary task retains sole final ownership |
| Level 2 | Visible primary task plus visible delivery tasks and necessary Level 1 subagents | Delivery needs durable identity, state, independent ownership, or user addressability |

Use Level 1 only when all conditions hold:

- It can finish before the current primary task ends.
- The primary task retains sole final delivery ownership and integrates and accepts the result.
- The user does not need to enter, question, redirect, or resume the subtask directly.
- The full trace can be compressed into conclusions, patches, `file:line`, or verification evidence and then safely discarded.
- Failure permits safe redispatch without losing important business state.
- It needs no independent project, branch, worktree, long-running environment, or formal upstream/downstream handoff.
- It has no overlapping writes with another execution unit.

Choose Level 2 when any condition holds:

- State or execution history must survive across turns.
- The user must enter the task to question, redirect, or resume it.
- The work unit owns an independent deliverable.
- A downstream task must formally consume its interface, artifact, manifest, or acceptance result.
- It needs an independent project, branch, worktree, or long-lived environment.
- QA, Repair, or external waiting needs a recoverable, auditable process.
- The full history cannot be safely compressed and discarded.
- The work unit still has independent value after the primary task ends.

Complexity, duration, module count, file modification, model choice, and reasoning effort are signals, not sufficient decisions by themselves. When the user has explicitly chosen a work structure, that choice overrides the “start at Level 0” heuristic.

## Delegate execution within authorization

- For an implementation request, dispatch useful separable implementation to workers; the primary task owns requirements, key decisions, integration, and final acceptance. A read-only review does not replace delegating suitable implementation. Small or tightly coupled steps may remain Level 0.
- Assign the role explicitly. Implementation workers edit assigned files, run relevant checks, and return actual artifacts. Scouting and independent QA remain read-only. Plan-only requests stay read-only; delegation never expands authorization.
- Split long workflows into finite stages with bounded inputs, edit scope, acceptance checks, and compressed handoffs. Reassess remaining execution after each accepted stage rather than personally completing every later step after a single review. Follow the user's model policy in applicable instructions.
- Keep routine routing rationale in working state. Report required decisions, material blockers, meaningful milestones, and delivery under current host responsiveness requirements; execution must not rely on the user monitoring explanations.

## Make authorization boundaries explicit

- Explicitly invoking `$orchestrate-codex-sessions-en` with implementation intent authorizes the orchestrator to choose Level 0, Level 1, or create the necessary Level 2 visible tasks within the current local scope without asking for each task separately.
- Explicit invocation for planning, comparison, review, or recommendation remains read-only and does not authorize task creation or project changes.
- Implicit Skill activation does not expand authority: Level 0/1 may proceed; when Level 2 is needed, list the proposed visible tasks and obtain one confirmation. Do not ask again when the user has already requested multi-session, independent, or sidebar-visible tasks.
- When the user asks only for a plan, comparison, or recommendation, stop at read-only analysis and an orchestration proposal. Do not create visible tasks or modify the project.
- Once the user explicitly authorizes implementation, continue within the established local scope without repeatedly asking for the same permission.
- External writes, publishing, pushing, permission changes, destructive actions, and material scope expansion still require separate authorization.

## Declare routing before dispatch

Before the first delegation, output this table with one row per work unit. Do not replace it with prose or omit columns:

| Work unit | Level | Sidebar-visible | Execution carrier | Ownership | Depends on | Initial state | Mode / edit scope | Completion evidence |
|---|---|---|---|---|---|---|---|---|
| ... | 0 / 1 / 2 | yes / no | primary task / `spawn_agent` / visible task | primary / independent delivery | none / ... | ready / blocked / pending | ... | ... |

Distinguish internal disposable subagents from user-visible tasks, and distinguish “create now” from “run only after dependencies pass.” Level 1 requires no sidebar task. Do not claim Level 2 orchestration exists until its visibility gate passes.

For each delegated row, also declare the exact creation tool, tool-accepted model ID, reasoning effort, and the source of those choices. Complete the model gate below before dispatch; a display name or an OpenCodex setting alone is not creation evidence.

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
- Parallelize independent scouting or implementation when current rules permit it and write ownership is disjoint.
- A visible task is not file isolation. Serialize overlapping writes in a shared checkout. Parallel writes require non-overlapping ownership or separate worktrees.

### 2.1 Treat dependencies and handoffs as hard gates

- Declare `Depends on`, `Produces`, `Consumes`, `Handoff gate`, and `On success` for every task. Do not dispatch artifact-dependent tasks in parallel without these fields.
- A downstream visible task may be created early but must remain `blocked` until its dependency passes. Its brief may describe only the waiting condition; it must not implement, guess interfaces, or terminate with a superficial answer.
- Upstream completion does not authorize downstream start. The orchestrator must verify actual artifacts, test results, and unverified items, then send a structured handoff package and trigger the downstream task.
- Minimum handoff package:

```yaml
status: ready_for_handoff
produced: [artifact paths]
manifest: path or null
verification: [actual commands and results]
failed_or_unverified: [items]
next_task: canonical task name
next_action: exact consumption step
```

- The downstream task must ACK that consumed files exist, the manifest is readable, and interface or data versions match. Only then may it move to `running`; otherwise keep it blocked and create the smallest Repair.
- For asset pipelines, the manifest must map `source -> consumer` and include format checks such as alpha, dimensions, license, or checksum. Consumer UI must use manifest targets instead of guessing filenames or retaining stale assets.
- Monitor accepted handoff packages, not prose claiming completion. This applies to UI → QA, Core → UI, generated assets → integration, and equivalent pipelines.

### 3. Decide whether to create `AGENTS.md`

- Do not create `AGENTS.md` for Level 0 or a one-off read-only subagent merely for formality.
- Before Level 2, create or update the project-level `AGENTS.md` with product boundaries, ownership, prohibitions, gates, verification, and final Acceptance.
- Preserve existing user rules and add only the minimum project contract required.
- Read [templates.md](references/templates.md) when a template is needed.

### 3.1 Creation and model gate (Level 1 and Level 2)

- Read the selected carrier's current tool schema before creation. Its advertised models, effort levels, argument names, and authorization rules are authoritative; `spawn_agent` and visible-task tools may expose different model sets. Do not copy a model ID from one carrier into another without checking.
- For a requested non-GPT model, inspect the available OpenCodex routes and reasoning levels before falling back to GPT. When available, use OpenCodex's read-only model/injection/effort status or the local catalog and configuration. Distinguish configured availability from support in the active creation tool and successful execution; do not change global settings to satisfy a dispatch.
- Resolve a user-facing alias to the exact ID accepted by the chosen carrier. Example: `agy/gemini3.8 flash high` may resolve to `model: "google-antigravity/gemini-3.8-flash"` with effort `"high"`; verify both against current evidence. An OpenCodex setting such as `openai/gpt-6-luna` must not be passed to `spawn_agent` when that tool advertises only `gpt-6-luna`. Do not generally strip provider prefixes: routed non-GPT IDs may require them.
- Preserve the user's requested model and effort within current tool permissions. Distinguish user choices, OpenCodex preferred injection settings, parent-session inheritance, and catalog defaults. `xhigh` means Extra High, not `high`; an omitted effort must not be assumed to inherit an OpenCodex injection value. When an explicit override is permitted and needed, use the carrier's actual field (`reasoning_effort` for `spawn_agent`, `thinking` for visible-task tools when advertised) and the verified supported level.
- A model missing from `spawn_agent` is unavailable on that carrier, not necessarily unavailable through OpenCodex. Check another authorized carrier that offers it, while preserving the work-unit, visibility, and ownership rules. Do not silently promote Level 1 to a visible task, create an unauthorized task, or substitute GPT/another effort; if no permitted route satisfies the request, report the specific boundary and obtain the necessary choice.
- On creation failure, preserve the raw error and determine whether anything was created. Correct only the evidenced ID/argument mismatch, retaining the model intent and effort; retry once after rechecking the schema when non-creation is confirmed. For an unknown outcome, recover existing IDs/state before any retry. A repeated failure is a blocker, not permission to guess another model. After success, check the returned identity and available execution metadata; report requested versus actual model/effort, or mark actual values unverified.

### 4. Dispatch Level 1 subagents

- Use `spawn_agent` for internal disposable work that satisfies every Level 1 condition. Never use it to impersonate a Level 2 user-visible task.
- If the requested model is unavailable on the native subagent tool, an available, authorized bounded CLI worker may carry Level 1 under the same lifetime and ownership rules. Track its process/session ID, result path, exit status, and requested/actual model and effort. Use scoped write permissions for implementation and read-only permissions for QA; do not bypass sandbox or authorization limits. A CLI worker is not a sidebar-visible task.
- Before each `spawn_agent` call, its routing row must explicitly say `Level 1`, `Sidebar-visible: no`, and `Execution carrier: spawn_agent`.
- Dispatch concrete, independent, well-bounded execution. For an authorized implementation request, assign explicit write scope and require actual changes, runnable checks, and artifacts; do not default it to advice or read-only review. Scouting and independent QA remain read-only. The primary task retains final ownership, integrates the result, and verifies it.
- Make every brief self-contained with search scope, exact question, allowed edit scope, and output format. Require `file:line`, symbol names, essential excerpts, patches, or source links.
- Parallelize independent questions only when current rules allow it. Never modify overlapping files concurrently. Follow the tool's required wait behavior.
- Treat a subagent result as a lossy compressed deliverable. Spot-check cited locations without rereading the entire delegated scope.
- Before the primary task responds finally, wait for and accept every Level 1 result. Do not leave a disposable subagent with future responsibility.
- When Level 1 discovers that work needs cross-turn state, direct user intervention, independent ownership, formal handoff, or long-term recovery, it must stop implementation and return current findings, artifacts, promotion reason, and next action. The primary task creates Level 2 when authorized; the subagent must not silently become a long-lived branch.
- A Level 2 visible task may still use Level 1 subagents that meet these rules.

### 5. Dispatch visible delivery tasks

- Write self-contained task briefs. Do not assume a new task inherits all primary-task history.
- Include the project path, upstream state, ownership, prohibited scope, Acceptance, verification commands, and required completion report.
- Resolve only the real project, host, environment, branch, and model values actually needed. When using a project, query its real identity and Git properties. Never invent project IDs, thread IDs, host IDs, models, branches, or worktree state. Do not perform irrelevant project lookup for projectless or fork flows.
- Use tools that create or fork user-visible tasks and apply the shared creation/model gate. If its permitted recovery fails or the capability is unavailable, stop and explain. Do not downgrade to `spawn_agent` without user approval.
- At the first Level 2 checkpoint, use the task list to confirm every target really exists and verify thread ID, title, project, environment, and status. Report `pending` when only a client ID exists or setup is queued; do not claim readiness. Read a task when possible to spot-check its brief.
- In full orchestrator mode, keep the primary task focused on management, decisions, and acceptance. Do not concurrently edit business code already owned by a delegated task.
- After each implementation task completes, verify scope, interfaces, check results, and downstream usability before starting dependent work.

### 6. Monitor and enforce gates

- Before waiting, accept returned results, prepare verification, or resolve independent decisions without duplicating delegated work or crossing write ownership. Wait when the next useful step depends on unfinished work.
- Track each work unit's real ID and carrier, dependencies, cursor when supported, latest progress evidence and time, blocker, delivery state, and next action. Use the compact state template in [templates.md](references/templates.md); keep it in working context unless durable handoff needs a saved record.
- Use the carrier's actual wait/snapshot tool; do not pass internal agent IDs to visible-thread tools. For visible tasks, batch active targets in one `wait_threads` call within the current limit (currently up to 8), preserving each target's host and returned cursor as `afterCursor`. For more targets, rotate bounded batches so one group cannot starve the others. Use `timeoutMs: 0` only for a needed immediate snapshot, not a busy loop.
- Separate a single wait's timeout from the interval for deeper diagnosis. Respect current tool and host limits; where a 60-second responsiveness limit applies, keep each blocking wait within it. Do not hard-code a 10-minute blocking call. Check startup blockers early and space deeper reads farther apart after demonstrated progress.
- Rely only on documented wake conditions. Current `wait_threads` wakes on completion, attention needed, or new user input; commentary alone does not wake it. Retain returned cursors and process per-target errors even when another target completes.

| Observation | Next action |
|---|---|
| A task returns a result | Inspect its report and evidence immediately; after acceptance, release only the downstream work whose dependencies pass. Do not wait for unrelated tasks. |
| Timeout with new progress | Record the evidence and cursor, then continue useful work or bounded waiting. Timeout is not task failure. |
| No new message, no confirmed blocker | Compare the expected operation with the latest tool activity and artifacts when needed. Silence or elapsed time alone does not prove a stall; do not repeatedly reread full history. |
| Input request, error loop, tool failure, or unmet dependency | Diagnose the specific blocker promptly within authorization. Leave user decisions to the user. Before retrying or reassigning, inspect existing artifacts and confirm the previous writer has stopped. |
| Execution ended without the required report | Record execution as ended and the report as missing; inspect artifacts and recover the report through the same task when authorized. Do not accept or restart the work merely because execution ended. |

- Distinguish execution ended, report returned, and primary-task acceptance. A self-declared completion is not acceptance: check actual changes, command output, artifacts, and unverified items.
- Remove ended executions from the active wait set while retaining any missing-report or acceptance action. After acceptance, release disposable Level 1 agents using the available lifecycle tool when no continuation is needed. Preserve visible Level 2 tasks; acceptance alone does not authorize archiving or deletion. Reuse the same work unit for an authorized direct continuation and re-add it only when running again.
- Report meaningful milestones, decisions, blockers, gate results, and repair closure; avoid repeating unchanged snapshots. Meet host communication requirements without inventing progress.
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
