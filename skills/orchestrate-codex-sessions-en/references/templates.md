# Orchestration Templates

Read and copy only the template required for the current task. Remove irrelevant placeholders. Do not introduce an abstraction for a single use.

## Pre-dispatch routing declaration

```text
Work unit: ...
Level: Level 0 / Level 1 / Level 2
Sidebar-visible: yes / no
Execution carrier: primary task / spawn_agent / visible task
Creation tool: exact current tool name / none
Model: tool-accepted ID / verified inherited default / none
Reasoning effort: supported level / verified inherited default / none
Model/effort evidence: user choice / current tool schema / OpenCodex read-only status
Ownership: primary task / independent delivery task
Depends on: none / ...
Initial state: ready / blocked / pending
Selection reason: whether the full trace is safely disposable and which state must persist
Completion evidence: ...
```

## Project-level AGENTS.md

```markdown
# Project Contract

## Product Goal
- Final user-visible result: ...
- Data source and key definitions: ...

## Global Boundaries
- Project root: ...
- Prohibited modifications: ...
- Privacy, network, permission, dependency, background-process, and publishing boundaries: ...
- Do not commit, push, or publish without authorization.

## Shared Rules
- Read this file before starting.
- Modify only files assigned to you.
- Do not revert or refactor another task's work.
- Report upstream issues without crossing ownership boundaries to fix them.
- On completion, list changed files, verification commands, actual results, and remaining issues.

## Ownership

### Core
- Owns: ...
- Must not edit: ...
- Prerequisites: ...
- Deliverables: ...
- Verification: ...

### UI
- Owns: ...
- Must not edit: ...
- Prerequisites: Core gate passed
- Deliverables: ...
- Verification: ...

### Package & QA
- Owns: packaging, real-data checks, visible UI, runtime, and security acceptance
- Must not edit: Core or UI implementation
- Prerequisites: runnable artifact
- Deliverables: QA report and final artifact
- Verification: ...

## Acceptance
- User-visible result: ...
- Data correctness: ...
- Build and runtime: ...
- Security and privacy: ...
- Report every unverified item explicitly.
```

## Level 1 subagent brief

```text
Complete a temporary subtask within [explicit directory, module, or source scope].

Mode: read-only scouting / verification / tightly bounded short-lived implementation
May edit: none / [explicit files]
The primary task retains final delivery ownership.

Exact question:
[Write one independently answerable question only.]

Return:
1. Conclusion;
2. file:line, symbol name, essential excerpt, or source link;
3. Risks directly relevant to the conclusion;
4. Unconfirmed items.

Do not expand into adjacent questions, modify unauthorized files, or return large raw logs.
If the work needs cross-turn state, direct user intervention, independent ownership, formal handoff, or long-term recovery, stop and return current findings, generated artifacts, promotion reason, and recommended next action.
```

## Level 2 visibility checkpoint

```text
Target task: ...
Creation result: READY / PENDING / FAILED
Requested model / effort: ...
Actual model / effort: ... / unverified
thread ID: ...
client ID, if any: ...
Task-list check: title / project / environment / status
Content spot-check: PASS / FAIL / not readable yet
Decision: START / WAIT / STOP
```

## Visible implementation task brief

```text
You own [one responsibility].

Project: ...
Before starting:
1. Read the project-level AGENTS.md;
2. Check upstream deliverables and current workspace state;
3. If a prerequisite is missing, report it without modifying upstream scope.

Ownership:
- May edit: ...
- Must not edit: ...

Required work:
- ...

Required verification:
- Commands: ...
- Scenarios: normal, boundary, failure, real data, or visible UI as applicable.

Completion report:
- Changed files;
- Verification commands and actual results;
- Unverified items and reasons;
- Remaining risks.

You are not alone in the codebase. Do not revert other people's changes. Adapt to the current workspace state.
```

## Read-only QA brief

```text
You own acceptance for [packaging / real data / visible UI / runtime / security] only.

Do not modify Core, UI, tests, or build logic. Do not create shims, bypass permissions, or fabricate a pass.

For each item return:
- Acceptance criterion;
- Evidence and actual result;
- PASS / DEFECT / ENV BLOCK;
- For DEFECT: file:line, reproduction, expected behavior, actual behavior, and impact;
- For ENV BLOCK: raw error, affected scope, and the boundary of what remains confirmed.
```

## Repair brief

```text
Fix only this confirmed root cause:
[Defect, reproduction, expected behavior]

May edit: ...
Must not edit: anything else.

Requirements:
1. Reproduce first;
2. Make the smallest fix at the shared root cause;
3. Leave one minimal regression check;
4. Do not refactor adjacent code, add dependencies, or commit.

Return changed files, exact change, verification result, and remaining limitations.
```

## Compact monitoring state

Keep one entry per work unit in working context; save it only when durable handoff requires it. These are bookkeeping fields, not tool arguments or invented runtime statuses. Omit unsupported optional fields.

```text
Work unit: real ID / carrier / host if applicable
Depends on: unmet dependencies or none
Cursor: last returned cursor, if supported
Last progress: timestamp / tool activity or artifact evidence
Blocker: none / evidence and required decision
Delivery: execution active or ended / report missing or returned / acceptance pending, passed, or failed
Next action: work / wait / diagnose / recover report / accept / hand off / release
```

## Primary-task gate report

```text
Stage: ...
Scope check: PASS / FAIL
Interface and artifact: PASS / FAIL
Verification evidence: ...
Unverified items: ...
Decision: NEXT / REPAIR / ENV BLOCK
Single next action: ...
```
